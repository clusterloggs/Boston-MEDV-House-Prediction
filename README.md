# Boston-House-MEDV-prediction

### Software and the tools Requirements

1. [Github Account](https://github,com)
2. [VS code IDE](https://code.visualstudio.com)
3. [Heroku Account](https://heroku.com)
4. [GitCLI](https://git-scm.com/book/en/v2/Getting-Started-The-Command_line)

Create a new environment

```
py -3.7 -m venv venv
```

Activate the venv environment that was created
```
venv\Scripts\activate
```

### Successful Docker Deployment to Heroku
#### Proper Docker Tagging
Tagged Docker image correctly to match the Heroku container registry format:

```
docker tag <image_name> registry.heroku.com/<app_name>/web
```
### Correct Heroku Commands for Container Deployment
Instead of pushing with docker push, we used Heroku’s container CLI commands to ensure proper build and release:
```
heroku container:push web --app <app_name>
heroku container:release web --app <app_name>
```
### Fixed CMD in Dockerfile
Avoided using exec form with $PORT which doesn't expand environment variables.
- Correct shell form used in Dockerfile:
```
CMD gunicorn --workers=4 --bind 0.0.0.0:$PORT app:app
```

### Used Logs to Debug
Monitored Heroku logs to identify runtime errors and crashes:
```
heroku logs --tail --app <app_name>
```

This helped to catch the $PORT substitution issue and fix it.

### Valid Project Structure
- Flask app was properly configured in app.py.
- Dependencies listed correctly in requirements.txt.
- Dockerfile used a compatible base image (python:3.7) with no build errors.