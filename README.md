# Kageかげ

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/B0B1Z3IGW)

**kage** — is the authentication and authorization system BuzzFeed developed to provide a secure, single sign-on experience

It depends on Google as its authoritative OAuth2 provider, and authenticates
users against a specific email domain. Further authorization based on Google
Group membership can be required on a per-upstream basis.

The main idea behind **sso** is a "double OAuth2" flow, where `kage-auth` is the
OAuth2 provider for `kage-proxy` and Google is the OAuth2 provider for `kage-auth`.

[kage](https://github.com/andikaleonardo/kage) is built on top of Bitly’s open source [oauth2_proxy](https://github.com/bitly/oauth2_proxy)

## Project Structure
```console
kage/
├── Cargo.toml
├── src/
│   ├── main.rs
│   ├── server.rs
│   ├── handler.rs
│   ├── user.rs
│   ├── db.rs
│   ├── token.rs
│   ├── error.rs
├── .env
```

## Pattern
```console
            +---------------------+
            |        Client       |
            +----------+----------+
                       |
                       | HTTP Requests
                       v
            +----------+----------+
            |    HTTP Server      |
            +----------+----------+
                       |
                       | Request Handling
                       v
            +----------+----------+
            |   Request Handler   |
            +----------+----------+
                       |
                       | Business Logic
                       v
   +-----------+--------------+-----------+
   |    Authentication          Database  |
   |    Middleware              (Redis)   |
   +--------------------------------------+

```

## Running the Project

### Prerequisites

Ensure Redis is running locally or on a server. You can use Docker to run Redis locally:
```sh
docker run --name redis -p 6379:6379 -d redis
```

Set up the .env file with the necessary environment variables:
```env
REDIS_URL=redis://127.0.0.1/
SECRET_KEY=your_secret_key
```

### Build and Run

Clone the repository:
```sh
git clone https://github.com/andikaleonardo/kage.git
cd kage
```

Build the project:
```sh
cargo build
```

Run the project:
```sh
cargo run
```

## Contributing

🎈 Thanks for your help improving the project! We are so happy to have
you! We have a [contributing guide][contributing] to help you get involved in the
`kage` project.

## License

This project is licensed under the [MIT license][license].

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in `kage` by you, shall be licensed as MIT, without any
additional terms or conditions.


[contributing]: https://github.com/tokio-rs/axum/blob/main/CONTRIBUTING.md
[license]: https://github.com/tokio-rs/axum/blob/main/axum/LICENSE
