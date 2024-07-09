
# Decentralized Real Estate Management Platform

This project is a decentralized platform built on the Internet Computer for managing real estate properties, lease agreements, and maintenance requests. The platform ensures secure, transparent, and efficient management of real estate assets and interactions.

## Key Features

### Property Management
- **Add Property**: Allows users to create property listings.
- **Get All Properties**: Retrieve a list of all properties.

### Lease Agreement Management
- **Add Lease Agreement**: Allows users to create lease agreements for properties.
- **Get All Lease Agreements**: Retrieve a list of all lease agreements.

### Maintenance Request Management
- **Add Maintenance Request**: Allows users to create maintenance requests for properties.
- **Get All Maintenance Requests**: Retrieve a list of all maintenance requests.

## Data Structures

### Property
```rust
struct Property {
    id: u64,
    address: String,
    owner: String,
    valuation: f64,
    status: String,
    created_at: u64,
}
```

### Lease Agreement
```rust
struct LeaseAgreement {
    id: u64,
    property_id: u64,
    tenant: String,
    rent: f64,
    start_date: u64,
    end_date: u64,
    created_at: u64,
    digital_signature: String,
}
```

### Maintenance Request
```rust
struct MaintenanceRequest {
    id: u64,
    property_id: u64,
    description: String,
    status: String,
    created_at: u64,
    priority: String,
}
```


## Requirements
* rustc 1.64 or higher
```bash
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
$ source "$HOME/.cargo/env"
```
* rust wasm32-unknown-unknown target
```bash
$ rustup target add wasm32-unknown-unknown
```
* candid-extractor
```bash
$ cargo install candid-extractor
```
* install `dfx`
```bash
$ DFX_VERSION=0.15.0 sh -ci "$(curl -fsSL https://sdk.dfinity.org/install.sh)"
$ echo 'export PATH="$PATH:$HOME/bin"' >> "$HOME/.bashrc"
$ source ~/.bashrc
$ dfx start --background
```

If you want to start working on your project right away, you might want to try the following commands:

```bash
$ cd icp_rust_boilerplate/
$ dfx help
$ dfx canister --help
```

## Update dependencies

update the `dependencies` block in `/src/{canister_name}/Cargo.toml`:
```
[dependencies]
candid = "0.9.9"
ic-cdk = "0.11.1"
serde = { version = "1", features = ["derive"] }
serde_json = "1.0"
ic-stable-structures = { git = "https://github.com/lwshang/stable-structures.git", branch = "lwshang/update_cdk"}
```

## did autogenerate

Add this script to the root directory of the project:
```
https://github.com/buildwithjuno/juno/blob/main/scripts/did.sh
```

Update line 16 with the name of your canister:
```
https://github.com/buildwithjuno/juno/blob/main/scripts/did.sh#L16
```

After this run this script to generate Candid.
Important note!

You should run this script each time you modify/add/remove exported functions of the canister.
Otherwise, you'll have to modify the candid file manually.

Also, you can add package json with this content:
```
{
    "scripts": {
        "generate": "./did.sh && dfx generate",
        "gen-deploy": "./did.sh && dfx generate && dfx deploy -y"
      }
}
```

and use commands `npm run generate` to generate candid or `npm run gen-deploy` to generate candid and to deploy a canister.

## Running the project locally

If you want to test your project locally, you can use the following commands:

```bash
# Starts the replica, running in the background
$ dfx start --background

# Deploys your canisters to the replica and generates your candid interface
$ dfx deploy
```