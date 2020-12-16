# paraphrase-service

A flask-based Docker image providing a deep-learning paraphrase service (text in, text paraphrases out).


## Installation

A conda env is provided. Simply execute:

```
conda env create -f environment.yml
```
followed by:

```
conda activate paraphrase
```
The `t5_paraphrase` model folder is not distributed and must be created.
See **TODO** for steps to create your own model.

## Server

The server is contained in `app.py`, so all modifications should be made there.

To run the server using flask, do:

```
export FLASK_APP=app.py
flask run
```

The Dockerfile in specifies a build using [Gunicorn](https://flask.palletsprojects.com/en/1.1.x/deploying/wsgi-standalone/) for production.
You can build a docker image with e.g.:

```
docker build --tag paraphrase-service:1.0 .
```

and run with, e.g.:

```
docker run -p 8000:8000 paraphrase-service:1.0
```

[Postman](https://learning.postman.com/) tests are in `paraphrase.postman_collection.json`, with different ports for flask and gunicorn (5000 for flask, 8000 for gunicorn).
These tests document how to call the server, but essentially it is POSTing JSON like this:

```json
{
    "sentence":"Epithelial tissue, also referred to as epithelium, refers to the sheets of cells that cover exterior surfaces of the body, line internal cavities and passageways, and form certain glands."
}
```
