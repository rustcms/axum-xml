# 使用
添加到 Cargo.toml
rustcms-axum-xml = "0.3.0"


# Extractor example

```rust
use axum::{
    extract,
    routing::post,
    Router,
};
use serde::Deserialize;
use rustcms_axum_xml::Xml;
///
#[derive(Deserialize)]
struct CreateUser {
    email: String,
    password: String,
}
///
async fn create_user(Xml(payload): Xml<CreateUser>) {
    // payload is a `CreateUser`
}
```



# Response example

```rust
use axum::{
    extract::Path,
    routing::get,
    Router,
};
use serde::Serialize;
use uuid::Uuid;
use rustcms_axum_xml::Xml;

#[derive(Serialize)]
struct User {
    id: Uuid,
    username: String,
}

async fn get_user(Path(user_id) : Path<Uuid>) -> Json<User> {
    let user = find_user(user_id).await;
    Xml(user)
}
```

# 新版 rustcms-axum-xml

因 axum-xml 0.2.0 不支持新版 axum ,所以在他基础上修改，并参考 axum Json 进行处理 Xml


XML extractor for axum.

This crate provides struct `Xml` that can be used to extract typed information from request's body.

Under the hood, [quick-xml](https://github.com/tafia/quick-xml) is used to parse payloads.

## Features

- `encoding`: support non utf-8 payload

## License

MIT