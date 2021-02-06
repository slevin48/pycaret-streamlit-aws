# Deploy PyCaret and Streamlit app using serverless infrastructure on AWS Fargate
#### A step-by-step tutorial to containerize machine learning app and deploy it using serverless infrastructure

Read the complete post: https://medium.com/@moez_62905/deploy-pycaret-and-streamlit-app-using-aws-fargate-serverless-infrastructure-8b7d7c0584c2

- Official Website : https://www.pycaret.org

- Follow us on LinkedIn : https://www.linkedin.com/company/pycaret/

- Subscribe to our YouTube : https://www.youtube.com/channel/UCxA1YTYJ9BEeo50lxyI_B3g 

- PyCaret repository : https://www.github.com/pycaret/pycaret


## Run docker locally

```
docker build -t pycaret-streamlit-aws .
docker run -d -p 8501:8501 pycaret-streamlit-aws
```

## Deploy Streamlit Docker on Heroku

In order to deploy this on heroku, there's a need to assign the port where streamlit will run with the `$PORT` environmental variable
https://help.heroku.com/PPBPA231/how-do-i-use-the-port-environment-variable-in-container-based-apps

One way to do that is to pass the port as flags on the command line when running streamlit run:
```
streamlit run your_script.py --server.port $PORT
```
https://docs.streamlit.io/en/stable/streamlit_configuration.html#set-configuration-options

(TODO: we might also try to specify the port in the global config file at ~/.streamlit/config.toml)

Concretely, modify line 21 of the [Dockerfile](Dockerfile):
`CMD streamlit run app.py --server.port $PORT`
