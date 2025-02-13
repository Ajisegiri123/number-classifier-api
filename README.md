"Development and Deployment of a Number Classification API with Mathematical Insights and Fun Facts". HNG task 1."

## **Overview**
The Number Classification API is a lightweight and efficient HTTP-based service designed to classify numbers based on their mathematical properties. This API is deployed using AWS Lambda and API Gateway, ensuring a serverless, cost-effective, and highly scalable architecture. By leveraging cloud-native technologies, the API delivers seamless performance while remaining publicly accessible, making it an ideal solution for real-time number classification and mathematical analysis.

## **Features**


1. **Mathematical Property Calculation:** Determines whether a number is prime, odd, armstrong, perfect, digit sum etc.
2. **Fun Fact Retrieval:** Fetches a fun fact about the number from an external API
3. Supports multiple number classifications in a single request.
4. ** JSON:** based responses.
5. ** CORS:**enabled for public access.
6. ** Deployment:** Must be deployed to a publicly accessible endpoint.

## **Architecture Diagram.**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5am9gtn6y9u83jmbcfb0.jpg)

**This API is deployed using:**

AWS Lambda for serverless execution.
API Gateway for exposing the endpoint.
GitHub for version control.

**Technologies Used:**
Python (Lambda function)
AWS Lambda (Serverless execution)
API Gateway (Public API exposure)
GitHub (Version control and CI/CD)

**Project Structure**

```
Number-Classification-API/
│-- lambda_function.py  # Main Lambda function
│-- requirements.txt    # Python dependencies
│-- README.md           # Project documentation
│-- .gitignore          # Git ignore file
└── app.py              # Python scripts
```
**Setting up**
Create a folder for your project.

Open the folder on your VScode editor.

create app.py and lambda-function.py files.

Open your github account and create a repository (Number-Classifier-API).

**Set up Instructions**

Clone the Repository

```
git clone https://github.com/Ajisegiri123/number-classifier-api.git

```
**- Change your directory to the project folder and then to your repository on your terminal.**

```
cd HNG-Task
cd number-classification-api
```

**Create and Activate Virtual Environment**

```
python -m venv venv
Source venv\Scripts\activate
```

**Install Dependencies**

```
pip install flask flask-cors
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2u4nvsfpegstxuzuw301.jpg)

**Create the Flask App**

Create a file called app.py in your project folder

```
from flask import Flask, request, jsonify
from flask_cors import CORS

app = Flask(__name__)
CORS(app)  # Enable CORS

# Function to check if a number is prime
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

# Function to check if a number is a perfect number
def is_perfect(n):
    return n == sum(i for i in range(1, n) if n % i == 0)

# Function to check if a number is an Armstrong number
def is_armstrong(n):
    digits = [int(d) for d in str(n)]
    power = len(digits)
    return n == sum(d**power for d in digits)

# Function to generate fun facts
def get_fun_fact(n):
    if is_armstrong(n):
        return f"{n} is an Armstrong number because {' + '.join([f'{d}^{len(str(n))}' for d in str(n)])} = {n}"
    elif is_prime(n):
        return f"{n} is a prime number because it has only two divisors: 1 and itself."
    elif is_perfect(n):
        return f"{n} is a perfect number because the sum of its proper divisors equals the number."
    else:
        return f"{n} is just an interesting number!"

@app.route('/api/classify-number', methods=['GET'])
def classify_number():
    num = request.args.get('number')

    if not num or not num.isdigit():
        return jsonify({"number": num, "error": True}), 400

    num = int(num)

    response = {
        "number": num,
        "is_prime": is_prime(num),
        "is_perfect": is_perfect(num),
        "properties": ["odd" if num % 2 else "even"],
        "digit_sum": sum(int(d) for d in str(num)),
        "fun_fact": get_fun_fact(num)
    }

    if is_armstrong(num):
        response["properties"].append("armstrong")

    return jsonify(response)

if __name__ == '__main__':
    app.run(debug=True)
```



# Function to check if a number is prime
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

# Function to check if a number is a perfect number
def is_perfect(n):
    return n == sum(i for i in range(1, n) if n % i == 0)

# Function to check if a number is an Armstrong number
def is_armstrong(n):
    digits = [int(d) for d in str(n)]
    power = len(digits)
    return n == sum(d**power for d in digits)

# Function to generate fun facts
def get_fun_fact(n):
    if is_armstrong(n):
        return f"{n} is an Armstrong number because {' + '.join([f'{d}^{len(str(n))}' for d in str(n)])} = {n}"
    elif is_prime(n):
        return f"{n} is a prime number because it has only two divisors: 1 and itself."
    elif is_perfect(n):
        return f"{n} is a perfect number because the sum of its proper divisors equals the number."
    else:
        return f"{n} is just an interesting number!"

@app.route('/api/classify-number', methods=['GET'])
def classify_number():
    num = request.args.get('number')

    if not num or not num.isdigit():
        return jsonify({"number": num, "error": True}), 400

    num = int(num)
    
    response = {
        "number": num,
        "is_prime": is_prime(num),
        "is_perfect": is_perfect(num),
        "properties": ["odd" if num % 2 else "even"],
        "digit_sum": sum(int(d) for d in str(num)),
        "fun_fact": get_fun_fact(num)
    }

    if is_armstrong(num):
        response["properties"].append("armstrong")

    return jsonify(response)

if __name__ == '__main__':
    app.run(debug=True)

Run the API Locally
python app.py
Image description

Open your browser to test the API:

http://127.0.0.1:5000/api/classify-number?number=153
JSON Response

Image description

Deploy the API
Create lambda_function.py

import json

def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

def is_perfect(n):
    return n == sum(i for i in range(1, n) if n % i == 0)

def is_armstrong(n):
    digits = [int(d) for d in str(n)]
    power = len(digits)
    return n == sum(d**power for d in digits)

def get_fun_fact(n):
    if is_armstrong(n):
        return f"{n} is an Armstrong number because {' + '.join([f'{d}^{len(str(n))}' for d in str(n)])} = {n}"
    elif is_prime(n):
        return f"{n} is a prime number because it has only two divisors: 1 and itself."
    elif is_perfect(n):
        return f"{n} is a perfect number because the sum of its proper divisors equals the number."
    else:
        return f"{n} is just an interesting number!"

def lambda_handler(event, context):
    try:
        query_params = event.get("queryStringParameters", {})
        num = query_params.get("number", "")

        if not num.isdigit():
            return {
                "statusCode": 400,
                "headers": {
                    "Content-Type": "application/json",
                    "Access-Control-Allow-Origin": "*"
                },
                "body": json.dumps({"number": num, "error": True})
            }

        num = int(num)

        response = {
            "number": num,
            "is_prime": is_prime(num),
            "is_perfect": is_perfect(num),
            "properties": ["odd" if num % 2 else "even"],
            "digit_sum": sum(int(d) for d in str(num)),
            "fun_fact": get_fun_fact(num)
        }

        if is_armstrong(num):
            response["properties"].append("armstrong")

        return {
            "statusCode": 200,
            "headers": {
                "Content-Type": "application/json",
                "Access-Control-Allow-Origin": "*"
            },
            "body": json.dumps(response)
        }

    except Exception as e:
        return {
            "statusCode": 500,
            "headers": {
                "Content-Type": "application/json",
                "Access-Control-Allow-Origin": "*"
            },
            "body": json.dumps({"error": str(e)})
        }

**>Run the API Locally**

```
python app.py
```

**>Open your browser to test the API:**

```
http://127.0.0.1:5000/api/classify-number?number=153
```
**JSON Response**


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hx14ony1rgs9twkprnvc.jpg)

**Deploy the API**

```
import json

def is_prime(n):
    if n < 2 or n % 1 != 0:  # Exclude negative and non-integer values
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

def is_perfect(n):
    if n <= 0 or n % 1 != 0:  # Exclude zero and non-integers
        return False
    return n == sum(i for i in range(1, int(n)) if n % i == 0)

def is_armstrong(n):
    if n % 1 != 0:  # Only consider integers
        return False
    digits = [int(d) for d in str(abs(int(n))) if d.isdigit()]
    power = len(digits)
    return n == sum(d**power for d in digits)

def get_fun_fact(n):
    if is_armstrong(n):
        return f"{n} is an Armstrong number because {' + '.join([f'{d}^{len(str(abs(int(n))))}' for d in str(abs(int(n))) if d.isdigit()])} = {n}"
    elif is_prime(n):
        return f"{n} is a prime number because it has only two divisors: 1 and itself."
    elif is_perfect(n):
        return f"{n} is a perfect number because the sum of its proper divisors equals the number."
    else:
        return f"{n} is just an interesting number!"

def lambda_handler(event, context):
    try:
        query_params = event.get("queryStringParameters", {})
        num = query_params.get("number", "")

        try:
            num = float(num)  # Convert input to float
        except ValueError:
            return {
                "statusCode": 400,
                "headers": {
                    "Content-Type": "application/json",
                    "Access-Control-Allow-Origin": "*"
                },
                "body": json.dumps({"number": num, "error": "Invalid number"})
            }

        response = {
            "number": num,
            "is_prime": is_prime(num),
            "is_perfect": is_perfect(num),
            "properties": [],
            "digit_sum": sum(int(d) for d in str(abs(int(num))) if d.isdigit()) if num % 1 == 0 else None,
            "fun_fact": get_fun_fact(num)
        }

        # Assign correct properties
        if num % 1 == 0:  # Only process whole numbers
            response["properties"].append("odd" if int(num) % 2 else "even")
            if is_armstrong(num):
                response["properties"].append("armstrong")

        return {
            "statusCode": 200,
            "headers": {
                "Content-Type": "application/json",
                "Access-Control-Allow-Origin": "*"
            },
            "body": json.dumps(response)
        }

    except Exception as e:
        return {
            "statusCode": 500,
            "headers": {
                "Content-Type": "application/json",
                "Access-Control-Allow-Origin": "*"
            },
            "body": json.dumps({"error": str(e)})
        }
```
**Package and Deploy to AWS Lambda**

```
zip function.zip lambda_function.py
```

**Create an API gateway**

1. Choose HTTP API.
2. Add Integration → Choose Lambda Function. 
3. Select your Lambda function (number-classifier-aPI). 
4. Enter /api/classify-number as the route. 
5. Choose GET as the method.

Then Deploy.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ga3d25w6tamdy457r33p.jpg)

**Test your API**

Once deployed, copy the API Gateway URL and test it in your browser

```
https://127.0.0.1:5000/api/classify-number?number=1895
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ewmcmxbf06eiecnv3419.jpg)

**Enable CORS in API Gateway.**

**Significance of the project.**

This project serves as a practical platform for developing and demonstrating core DevOps competencies. Despite its simplicity, it provides hands-on experience in building, deploying, and managing a real-world application, which is highly valuable in the industry. By implementing best practices and integrating advanced DevOps techniques, the project enhances technical proficiency, making it an excellent opportunity for skill development and showcasing expertise in modern software deployment and automation.
