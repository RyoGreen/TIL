# How to connect to Postgresql and how to get data
```
use chrono::DateTime;
use chrono_tz::Asia::Tokyo;
use tokio_postgres::{Client, Error, NoTls};

struct DbConfig {
    port: u32,
    host: String,
    user: String,
    password: String,
    database: String,
}

impl DbConfig {
    fn new() -> Self {
        DbConfig {
            port: 0,
            host: "".to_string(),
            user: "".to_string(),
            password: "".to_string(),
            database: "".to_string(),
        }
    }

    async fn connect(&self) -> Result<Client, Error> {
        let connection_str = format!(
            "host={} port={} user={} password={} dbname={}",
            self.host, self.port, self.user, self.password, self.database
        );

        let (client, connection) = tokio_postgres::connect(&connection_str, NoTls).await?;

        tokio::spawn(async move {
            if let Err(e) = connection.await {
                eprintln!("connection error: {}", e);
            }
        });

        Ok(client)
    }
}

struct User {
    id: i32,
    name: String,
    created_at: chrono::DateTime<chrono::Utc>,
    updated_at: chrono::DateTime<chrono::Utc>,
}

#[tokio::main]
async fn main() {
    let db_config = DbConfig::new();
    match db_config.connect().await {
        Ok(client) => {
            if let Err(e) = client.execute("SET search_path=***;", &[]).await {
                eprint!("Error setting search path: {}", e);
                return;
            }

            match client
                .query("select id,name,created_at,updated_at from users;", &[])
                .await
            {
                Ok(rows) => {
                    let mut users: Vec<User> = Vec::new();
                    for row in rows {
                        let id: i32 = row.get(0);
                        let name: String = row.get(1);
                        let created_at: DateTime<chrono::Utc> = row.get(2);
                        let updated_at: DateTime<chrono::Utc> = row.get(3);

                        users.push(User {
                            id,
                            name,
                            created_at,
                            updated_at,
                        });
                    }
                    for user in users {
                        println!(
                            "id: {}, name: {}, created_at: {}, updated_at: {}",
                            user.id,
                            user.name,
                            user.created_at.with_timezone(&Tokyo),
                            user.updated_at.with_timezone(&Tokyo)
                        )
                    }
                }
                Err(e) => {
                    eprintln!("Error executing query: {}", e);
                }
            }
        }
        Err(e) => {
            eprintln!("Error connecting to the database: {}", e);
        }
    }
}

```