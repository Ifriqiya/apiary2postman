apiary2postman
==============

Tool for generating a Postman collection from an API Blueprint, or an API Blueprint hosted on Apiary.

Supports

  * [API Blueprint](https://apiblueprint.org)
  * [API Blueprint AST](https://github.com/apiaryio/api-blueprint-ast), which can be generated by [Drafter](https://github.com/apiaryio/drafter)
  * Fetching an API Blueprint from Apiary API

    
# Prerequisites

[Drafter](https://github.com/apiaryio/drafter) < 2.0 is required if you want to use API Blueprint/Apiary API.

To install on OS X:

    brew install --HEAD https://raw.githubusercontent.com/apiaryio/drafter/b3dce8dda5d48b36e963abeffe5b0de7afecac3d/tools/homebrew/drafter.rb
    
To install from source:

    git clone https://github.com/apiaryio/drafter
    cd drafter
    git checkout b3dce8d # This is the commit for release 0.1.9
    git submodule update --init --recursive # Get all the dependencies needed for compile
    ./configure
    make
    sudo make install

Drafter is used to convert Blueprint API to JSON. The preferred version is v0.1.9.
Drafter v2 changed the JSON output format to be incomptabile with apiary2postman.
Feel free to submit a pull request which fixes this.

# Installation

    pip install apiary2postman

### Or, run from your checkout

    git clone <repo-url>
    cd apiary2postman/apiary2postman
    ./apiary2postman.py <args>

# Usage

    apiary2postman json blueprint.json --output postman.json

##### If you have the API Blueprint, use the `blueprint` subcommand:

    apiary2postman blueprint some.blueprint > postman.dump
  
It is also possible to pipe everything:

    cat some.blueprint | apiary2postman blueprint > postman.dump

##### To generate a total Postman environment dump from Apiary API, use the `api` subcommand with your Apiary API name:
 
    apiary2postman api my_api > my_api.dump

If you don't have an API key, go to https://login.apiary.io/tokens. Generate one if needed, and set the environment variable `APIARY_API_KEY` to that hex string.

    APIARY_API_KEY=ffffffffffffffffffffffffffffffff apiary2postman api my_api > my_api.dump

Or to generate only a Postman collection from Apiary API:

    apiary2postman --only-collection api my_api > my_api.collection

It's also possible to specify the output file using the `--output`.

##### If you have the API Blueprint AST already generated, use the `json` subcommand:

    apiary2postman json some.json > postman.dump
    
It is also possible to pipe everything:

    cat some.json | apiary2postman json > postman.dump

# Contribution

Contributions are greatly appreciated. What is most lacking is tests and would be super-grealy appreciated.
