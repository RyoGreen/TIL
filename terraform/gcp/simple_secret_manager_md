# secret manager
```
provider "google" {
  project = ""
  region  = "asia-northeast1"
  zone    = "asia-northeast1-a"
}

resource "google_secret_manager_secret" "secret-basic" {
  secret_id = ""

  labels = {
    label = "sample_label"
  }

  replication {
    auto {}
  }
}

resource "google_secret_manager_secret_version" "secret-version-basic" {
  secret      = google_secret_manager_secret.secret-basic.id
  secret_data = "this is secret data"
}
```