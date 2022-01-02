This project is created using following the <b>Full-text Search in Django with Postgres and Elasticsearch</b>  course at testdriven.io<br>
Course Link: https://testdriven.io/courses/django-full-text-search/

### Run
```zsh
docker-compose -f docker-compose.prod.yml up -d --build
```

### Load Data
Download the wines.zip file to the fixtures directory, unzip it, copy the JSON file to the directory, and then delete the ZIP file

```zsh
curl -o wines.zip https://raw.githubusercontent.com/testdrivenio/django-postgres-elasticsearch/master/wines.zip
unzip wines.zip
mv wines/wines.json .
rm -rf wines.zip
```
Load the data to postgres using the following commands:
```zsh
docker-compose exec server \
    python manage.py loaddata \
        catalog/fixtures/wines.json \
        --app catalog \
        --format json
```

### Create Superuser
```zsh
docker-compose exec server python manage.py createsuperuser
```

### Update elasticsearch index
```zsh
docker-compose exec server python manage.py elasticsearch
```

### Run Python Tests
```zsh
docker-compose exec server python manage.py test
```

### Run Cypress Tests
```zsh
npx cypress open --config baseUrl=http://localhost:8003
```