// Cargo.toml
// [dependencies]
// actix-web = "4"
// rand = "0.8"

use actix_web::{web, App, HttpServer, Responder, HttpResponse};
use rand::Rng;
use serde::{Deserialize, Serialize};

#[derive(Serialize)]
struct GameResult {
    result: String,
    winnings: u32,
}

async fn spin_wheel() -> impl Responder {
    let mut rng = rand::thread_rng();
    let roll = rng.gen_range(0..100);
    let (result, winnings) = if roll < 50 {
        ("Verloren", 0)
    } else if roll < 80 {
        ("Gewonnen", 10)
    } else {
        ("Jackpot!", 100)
    };
    
    HttpResponse::Ok().json(GameResult {
        result: result.to_string(),
        winnings,
    })
}

#[actix_web::main]
async fn main() -> std::io::Result<()> {
    HttpServer::new(|| {
        App::new()
            .route("/spin", web::get().to(spin_wheel))
    })
    .bind(("127.0.0.1", 8080))?
    .run()
    .await
}
****
