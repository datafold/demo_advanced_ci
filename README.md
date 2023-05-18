# data-diff-demo
Demo of data-diff with a dbt project using dbt-duckdb

## Prerequisites

Verify that `dbt`, `python3`, and `git` are installed and available:
```shell
dbt --version
python3 --version
git --version
```

## Clone

Clone this repo using HTTPS (or [your method of choice](docs/clone.md)):

```shell
git clone https://github.com/datafold/demo.git
cd demo
git checkout duckdb_demo
```

</details>

## Install
Create a virtual environment and install dependencies using `bash`/`zsh` (or [your OS shell of choice](docs/virtual-environment.md)):

```shell
python3 -m venv env
source env/bin/activate
python3 -m pip install --upgrade pip
python3 -m pip install -r requirements.txt
source env/bin/activate
unset DBT_PROFILES_DIR # applicable if you have a DBT_PROFILES_DIR variable set
```

## Setup

Establish the baseline production tables:
```shell
dbt build --full-refresh --target prod
```

Establish the baseline dev tables:
```shell
dbt build --full-refresh
```

## Usage

Simulate a change to the table during development:

Go to `models/core/dim_orgs.sql` and comment out the `prod` CTE for the `dev` CTE

Run a single model & diff
```
dbt run -s dim_orgs && data-diff --dbt
```

Run model + all downstreams & diff
```
dbt run -s dim_orgs+ && data-diff --dbt
```

## Wrap up
Deactivate the virtual environment when finished:

```shell
deactivate
```
