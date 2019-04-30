# Fast.ai hotdog classifier
> Serverless classifier trained with AWS Sagemaker and deployed on AWS Lambda

See blog post: https://medium.com/@pvhee/building-a-serverless-not-hotdog-classifier-with-aws-sagemaker-and-lambda-dd473cf6506a

## Model training

Check out the [Jupyter notebook](notebooks/hotdog.ipynb) for model training using [fast.ai](https://fast.ai) and make sure to save your model to AWS S3.


## Inference in production

We use the [serverless framework](https://www.serverless.com/) to get our model inference on AWS Lambda.

```
serverless deploy
...
endpoints:
  POST - https://ax45wn5lv2.execute-api.us-east-1.amazonaws.com/dev/invoke
```

Example inference on [this hotdog](https://leitesculinaria.com/wp-content/uploads/fly-images/96169/best-hot-dog-recipe-fi-400x300-c.jpg).

```
curl -d "{\"url\":\"https://leitesculinaria.com/wp-content/uploads/fly-images/96169/best-hot-dog-recipe-fi-400x300-c.jpg\"}" -H "Content-Type: application/json" -X POST https://ax45wn5lv2.execute-api.us-east-1.amazonaws.com/dev/invoke
```

## Load testing inference

We use [artillery.io](https://artillery.io/) to load test our model inference.

```
cd loadtest/
artillery run artillery.yml
```