# Password-Generator
Password Generator 

from flask import Flask, render_template_string 
import random
import string

app = Flask(__name__)

def generate_password(length=12):
    lowercase = string.ascii_lowercase
    uppercase = string.ascii_uppercase
    digits = string.digits
    punctuation = string.punctuation

    all_characters = lowercase + uppercase + digits + punctuation

    password = ''.join(random.choice(all_characters) for i in range(length))
    return password

@app.route('/')
def index():
    password = generate_password(16)
    return render_template_string('''
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Password Generator</title>
            <style>
                body {
                    font-family: Arial, sans-serif;
                    background-color: #f3f4f7;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    height: 100vh;
                    margin: 0;
                    text-align: center;
                }
                .container {
                    background-color: white;
                    padding: 30px;
                    border-radius: 8px;
                    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
                    width: 400px;
                }
                h1 {
                    font-size: 36px;
                    color: #4a90e2;
                    margin-bottom: 20px;
                }
                .password {
                    font-size: 24px;
                    font-weight: bold;
                    color: #333;
                    margin-bottom: 20px;
                    padding: 10px;
                    background-color: #e9e9e9;
                    border-radius: 4px;
                }
                .button {
                    background-color: #4a90e2;
                    color: white;
                    border: none;
                    padding: 10px 20px;
                    font-size: 18px;
                    border-radius: 5px;
                    cursor: pointer;
                    transition: background-color 0.3s ease;
                }
                .button:hover {
                    background-color: #357ab7;
                }
                .emoji {
                    font-size: 24px;
                }
            </style>
        </head>
        <body>
            <div class="container">
                <h1>Password Generator</h1>
                <div class="password">
                    <span class="emoji">🎉</span> <span>{{ password }}</span> <span class="emoji">🎉</span>
                </div>
                <button class="button" onclick="window.location.reload()">Generate New Password</button>
            </div>
        </body>
        </html>
    ''', password=password)

if __name__ == '__main__':
    app.run(debug=True)
