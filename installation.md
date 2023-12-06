## Install Commune

Based on my experience on EndeavourOS with [Docker](https://www.docker.com/get-started) already installed


- Clone commune repository
```sh
$ git clone git@github.com:commune-ai/commune.git
```

- Pull all required submodules
```sh
$ make pull  # git submodule update --init --recursive --force
```

Note: Docker didn't actually work right now so we'll revisit this in the future

- Build images
```sh
$ docker compose build
```

- Or just start the damn thing
```sh
$ docker compose up -d
```

- Exec into the commune container
```sh
.../commune $ docker compose exec commune bash
```

- Get a root key (store this shit)... But okay, we actually can't do anything without the subspace running so...
```sh
root@machine$~: c root_key
```

### Installing Commune Locally with Subspace

- Add `export PATH="$HOME/.cargo/bin:$PATH"` to your shell config
- Install _most_ Python deps to a pipenv (I saved at ~/repos/communeai/). Alternatively create your own venv then replace `pipenv` with `pip`.
```sh
$ pipenv install click numpy protobuf==3.20 streamlit
```
- Once the pipenv is created, enter it with `pipenv shell`, then go to the commune repo and install it. It will also install the rest of the dependancies.
```sh
$ cd commune  # git repo for commune
$ pip install -e ./
```
- Setup rust by installing rustup script
```sh
$ curl https://sh.rustup.rs -sSf | sh -s -- -y
$ rustup install nightly-2023-01-01  # has to be this version?
$ rustup override set nightly-2023-01-01
$ rustup target add wasm32-unknown-unknown
```
- **NOTE** If you came here from Docker setup, you will need to chown your `.commune` and `.bittensor` folders in your root directory back to your user (they will be root)
- Check commune is working
```sh
$ c modules
```
- Get your root key (keep this output somewhere safe)
```sh
$ c root_key
```
- Start the node
```sh
$ c start_local_node
$ c s n
```
- Set up something to run, using openrouter as example

