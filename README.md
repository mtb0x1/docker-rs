# what is this?
This repo is a fork of [this](https://github.com/ghmlee/rust-docker).

This repo is a Docker Remote API binding in Rust, the api documen docs is available [here](https://docs.docker.com/engine/api/).

Issues and PRs welcome.

## Quick start

```
[dependencies]
docker-rs = "0.1.0"
```

```rust
use docker_rs::Docker;

fn main() {
    let _ = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };
}
```

### Networks
```rust
use docker_rs::Docker;

fn main() {
    let mut docker = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };

    let networks = match docker.get_networks() {
        Ok(networks) => networks,
        Err(e) => { panic!("{}", e); }
    };
}
```


### Containers

```rust
use docker_rs::Docker;

fn main() {
    let mut docker = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };

    let containers = match docker.get_containers(false) {
        Ok(containers) => containers,
        Err(e) => { panic!("{}", e); }
    };
}
```

### Stats

```rust
use docker_rs::Docker;

fn main() {
    let mut docker = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };

    let containers = match docker.get_containers(false) {
        Ok(containers) => containers,
        Err(e) => { panic!("{}", e); }
    };

    let stats = match docker.get_stats(&containers[0]) {
        Ok(stats) => stats,
        Err(e) => { panic!("{}", e); }
    };
}
```

### Images

```rust
use docker_rs::Docker;

fn main() {
    let mut docker = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };

    let images = match docker.get_images(false) {
        Ok(images) => images,
        Err(e) => { panic!("{}", e); }
    };
}

```
### Info

```rust
use docker_rs::Docker;

fn main() {
    let mut docker = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };

    let info = match docker.get_system_info() {
        Ok(info) => info,
        Err(e) => { panic!("{}", e); }
    };
}
```

### Processes

```rust
use docker_rs::Docker;

fn main() {
    let mut docker = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };

    let containers = match docker.get_containers(false) {
        Ok(containers) => containers,
        Err(e) => { panic!("{}", e); }
    };

    let processes = match docker.get_processes(&containers[0]) {
        Ok(processes) => processes,
        Err(e) => { panic!("{}", e); }
    };
}
```

### Filesystem changes

```rust
use docker_rs::Docker;

fn main() {
    let mut docker = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };

    let containers = match docker.get_containers(false) {
        Ok(containers) => containers,
        Err(e) => { panic!("{}", e); }
    };

    let changes = match docker.get_filesystem_changes(&containers[0]) {
        Ok(changes) => changes,
        Err(e) => { panic!("{}", e); }
    };
}
```

### Export a container

```rust
use docker_rs::Docker;

fn main() {
    let mut docker = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };

    let containers = match docker.get_containers(false) {
        Ok(containers) => containers,
        Err(e) => { panic!("{}", e); }
    };

    let bytes = match docker.export_container(&containers[0]) {
        Ok(bytes) => bytes,
        Err(e) => { panic!("{}", e); }
    };
}
```

### Create an image

```rust
use docker_rs::Docker;

fn main() {
    let mut docker = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };

    let image = "debian".to_string();
    let tag = "latest".to_string();
    
    let statuses = match docker.create_image(image, tag) {
        Ok(statuses) => statuses,
        Err(e) => { panic!("{}", e); }
    };
    
    match statuses.last() {
        Some(last) => {
            println!("{}", last.clone().status.unwrap());
        }
        None => { println!("none"); }
    }
}
```

### Ping the docker server

```rust
use docker_rs::Docker;

fn main() {
    let mut docker = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };
    
    let ping = match docker.ping() {
        Ok(ping) => ping,
        Err(e) => { panic!("{}", e); }
    };
}
```

### Show the docker version information

```rust
use docker_rs::Docker;

fn main() {
    let mut docker = match Docker::connect("unix:///var/run/docker.sock") {
    	Ok(docker) => docker,
        Err(e) => { panic!("{}", e); }
    };
    
    let version = match docker.get_version() {
        Ok(version) => version,
        Err(e) => {panic!("{}",e)}
    };
}
```