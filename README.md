1.Create a basic python or php web server that says: hello word

For Python, we'll use the Flask framework to create a simple web server.

Python code (save it as app.py):

code
...........


from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, world!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)



To run this Python web server locally, you'll need to install Flask. Open a terminal or command prompt and execute the following commands:

 code 
.........
pip install flask
python app.py


You should see a message indicating that the server is running. You can access it in your browser by visiting http://localhost:5000, where you'll see the "Hello, world!" message.


2) Create a docker container for it.



To containerize the Python web server, we'll create a Dockerfile.

Dockerfile (save it as Dockerfile):


 code
..........
FROM python:3.9

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .

CMD [ "python", "app.py" ]

Create a file named requirements.txt in the same directory and add the following line:

 code
.............
Flask

Build the Docker image by running the following command in the terminal:


 code
.............
docker build -t my-web-server .
Once the build is complete, you can run the Docker container with:


 code
.............
docker run -p 5000:5000 my-web-server
You can access the web server in your browser by visiting http://localhost:5000, and you should see the "Hello, world!" message.


3) host it on an EC2 or free azure server.

Host on EC2 

To host the Docker container on an EC2 instance  you'll need to follow the respective platform's documentation to set up your server.

For EC2, you can refer to the AWS documentation on how to launch an EC2 instance and connect to it: https://docs.aws.amazon.com/efs/latest/ug/gs-step-one-create-ec2-resources.html


Once you have your server set up and connected, you'll need to install Docker on the server.

After Docker is installed, you can copy the Docker image you created earlier to the server using docker save and docker load commands or by pushing the image to a container registry like Docker Hub.

Finally, run the Docker container on the server using the same command as before:

 code
..............

docker run -p 5000:5000 my-web-server

Now you can access your Python web server hosted on EC2 or Azure by visiting the public IP or domain name of your server at port 5000 (http://<public-ip>:5000 or http://<domain-name>:5000), and you should see the "Hello, world!" message.














