# Actix web 1.x async/await shim.

## Usage

```rust
use actix_web::{web, App, HttpResponse, Error};
use std::time::{Instant, Duration};
use tokio::timer::Delay;
use actix_web_async_compat::async_compat;

async fn index() -> Result<HttpResponse, Error> {
    // wait 2s
    Delay::new(Instant::now() + Duration::from_secs(2)).await?;
    ok(HttpResponse::Ok().finish())
}

App::new().service(web::resource("/").route(
    web::to_async(async_compat(index)))
);
```
