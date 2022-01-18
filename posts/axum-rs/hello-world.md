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
    let app = Router::new()
    // .route("/", get(|| async { "Hello, World!" }));
        .route("/", get(root))
        .route("/foo", get(get_foo).post(post_foo))
        .route("/foo/bar", get(foo_bar));

    axum::Server::bind(&"0.0.0.0:3000".parse().unwrap())
    .serve(app.into_make_service())
    .await
    .unwrap();
}

async fn root() -> String {
    "get Root!".to_string()
}

async fn get_foo() -> String {
    "get Foo".to_string()
}

async fn post_foo() -> String {
    "post Foo".to_string()
}

async fn foo_bar() -> String {
    "get FooBar".to_string()
}

```

```
curl 127.0.0.1:3000
-> get Root!

GET /foo
-> get Foo

POST /foo
-> post Foo

GET /foo/bar
-> get FooBar
```