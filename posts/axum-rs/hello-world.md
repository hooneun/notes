# axum
[Document](https://docs.rs/axum/latest/axum/#examples)

`Cargo.toml`
```toml
[dependencies]
axum = "0.4.4"
tokio = { version = "1.15.0", features = ["full"] }
```

`main.rs`
```rs
use axum:{routing::get, Router};

#[tokio::main]
async fn main() {
    let app = Router::new().route("/", get(|| async { "Hello, World!" }));

    axum::Server::bind(&"0.0.0.0:3000".parse().unwrap())
    .serve(app.into_make_service())
    .await
    .unwrap();
}
```

```
curl 127.0.0.1:3000
-> Hello, World!
```