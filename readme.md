# Notice changes 
First error was in qr_service: change the import qrCode to import qrcode
Second error was in the main.py file change app.include_router(qr_code.ruter) to app.include_router(qr_code.router)
 
Local pytest ran
qr_code.py file line 24 changed from @router.post("/qr-coes/", response_model=QRCodeResponse, status_code=status.HTTP_200_OK, tags=["QR Codes"])
to 
@router.post("/qr-codes/", response_model=QRCodeResponse, status_code=status.HTTP_200_OK, tags=["QR Codes"])

Oauth.py line 18 @router.post("/tokn", response_model=Token) changed to 
@router.post("/token", response_model=Token)

This warning showed WARNING  root:common.py:36 Authentication failed for user: admin
So check the config.py and changed ADMIN_PASSWORD = os.getenv('ADMIN_PASSWORD', 'ecret') to ADMIN_PASSWORD = os.getenv('ADMIN_PASSWORD', 'secret')

Last test for schema.py line 5  ul: HttpUrl = Field(..., description="The URL to encode into the QR code.") changed to  url: HttpUrl = Field(..., description="The URL to encode into the QR code.")

Line 37  schema.py  changed from  mssage: str = Field(..., description="A message related to the QR code request.") to  message: str = Field(..., description="A message related to the QR code request.")
Line 69 common.py sanitizd_url = validate_and_sanitize_url(str(url)) changed to sanitized_url = validate_and_sanitize_url(str(url))
Line 70 common.py if sanitized_url is None: changed to if sanitized_url is None:
Line 72 common.py encoded_bytes = base64.urlsafe_b64encode(sanitized_url.encode('utf-8')) changed to  encoded_bytes = base64.urlsafe_b64encode(sanitized_url.encode('utf-8'))

Line 84 common.py  changed from decoded_bytes = base64.urlsafe_b6decode(encoded_str) to 
decoded_bytes = base64.urlsafe_b64decode(encoded_str)

line 24 qr_code.py changed from @router.post("/qr-codes/", response_model=QRCodeResponse, status_code=status.HTTP_200_OK, tags=["QR Codes"]) to @router.post("/qr-codes/", response_model=QRCodeResponse, status_code=status.HTTP_201_CREATED, tags=["QR Codes"])

Line 45 qr_code changed from status_code=status.HTTP_200_OK, changed to status_code=status.HTTP_409_CONFLICT,


# RestAPI for Creating QR Codes

For this assignment I want you to go over the videos and I've created a X number of errors in the code that you will have to find and fix them.  You should keep running the tests and read the error and try to understand what it mean.  The purpose of this assignment is to get you accustomed to running the project and following the steps that the program uses to process requests.

Here is my repo with the working code: [https://github.com/kaw393939/fastapi_spring2024](https://github.com/kaw393939/fastapi_spring2024)

You can get this repo working with the install instructions below.  The assignment repo will not work because its filled with broken code.

**To submit this assignment, you should make your own repository and add the remote to git and then push your fixed code to your own repo.** 

## Grading

You will only get 100 if the entire QR program passes GitHub actions, so you will need to update the production.yml file to have your info and setup your environment variables on the repository.

# Instructor Videos
* [Rest API Project Overview](https://youtu.be/xEcBKSSXxhQ)
* [QR Code Overview for Assignment](https://youtu.be/E6b9VkQpQ-U)


## Optional but extremely helpful:

1. [Best Series to Learn Bash Scripting Seriously learn this!!!](https://www.youtube.com/playlist?list=PLIhvC56v63IKioClkSNDjW7iz-6TFvLwS)

2.  [Listen to someone else explain FastAPI and go through a project](https://www.youtube.com/watch?v=cbASjoZZGIw)

# Install
1. Clone
2. Make virtual environment:  python3 -m venv venv
3. Activate virtual environment: source venv/bin/activate
4. Install requirements: pip install -r requirements.txt
5. **IMPORTANT** run: mkdir qr_codes to create a qr codes directory to save in, permissions will be messed up and the docker container won't be able to write to the qr_codes directory if you don't.
6. Note: make sure docker is started
7. run pytest locally to check that it works locally
8. Start the app with docker compose up --build
9. Goto http://localhost/docs to view openapi spec documentation
10. Click "authorize" input username: admin password: secret
11. Test making,  retrieving, and deleting QR codes on the spec page.