# A Novel Hybrid Multikey Cryptography Technique for Video Communication with Client-Server Model

Protecting copyright and preventing piracy has become a crucial concern in real-time video streaming systems. This research project presents a revolutionary multi-key and hybrid cryptography approach to provide enhanced security for video communication.

The project implements a software solution for video encryption and decryption using a continuous system based on the Elliptic Curve Cryptography (ECC) approach as pseudorandom encryption key generators. This approach generates multiple keys to encrypt and decrypt small chunks of video files dynamically, based on the video data. The implementation follows a client-server model utilizing socket programming.

### Video Walkthrough
<video width="100%" height="100%" controls>
  <source src="assets/demo.webm" type="video/mp4">
  Your browser does not support the video tag
</video>


## Project Flow

1. User Registration:
   - Users register on a web page developed using Flask.
   - User data is stored in a SQLAlchemy database.
   - During registration, users are required to import their public key and provide their email, password, and MAC address.

2. User Login and Dashboard:
   - Users log into the web page using their credentials.
   - Upon successful login, the user's dashboard displays video thumbnails.
   - The dashboard provides a download button to obtain the client software used to connect to the streaming server.

3. Client Execution:
   - Users execute the `client.py` script on their local machine.
   - The server prompts the user to enter their email and password for verification.
   - If the provided credentials match those used during registration, the server displays the list of videos available, which corresponds to the videos displayed on the user's dashboard.

4. Additional Authentication:
   - The user is asked to enter their MAC address, which was provided during registration, to ensure further security.

5. Private Key Import:
   - The user is prompted to import their private key path to decrypt the received video from the server.

6. Video Decryption and Playback:
   - Once the decryption process is completed, the video is immediately played for the user.

## Encryption Flow

The video file encrypion flow as follows.

```
1. Input video file Vinput
2. Generate video chunks Vci from Vinput
3. Fetch the receiver's public key of the RPkey
4. Collect receiver's MAC address Rmac
5. Generate VID using Vc0
6. Store VID in a temporary file
7. Encrypt Vc0 using RSA
8. Generate Keya ← x^3 + VID * x + Rmac
9. Encrypt Vc1 using Keya and AES
10. for i := 2 to n do
11.    Generate Keya ← x^3 + Keya * x + Rmac
12.    Encrypt Vci using Keya and AES
13. end for
```

## Internal Processes:

- User Registration:
   - During registration, users are required to import their public key, along with their email, password, and MAC address.
- Encryption

![Video Encryption](assets/video_encryption.png)

   - The server-side encryption involves AES encryption of each 1MB chunk of the video file.

![keygeneration](assets/keygeneration.png)

   - The encryption key used for AES is generated using a novel key generation technique that combines RSA and ECC.
- Decryption
   - The decryption was done at the client side same key generation was used here.

## Analysis of Results

### Time to generate keys

To determine the impact of the multi-key in the encryption and decryption process, the time required to generate the key was calculated in this experiment. The method and equation used to derive the keys are the same for both encryption and
decryption. So, for the sake of analysis, the delay calculated for encryption has been employed in this part. The receiver’s public key and partial video data serve as the basis for the key used to encrypt the first video chunk. The remaining keys are obtained using the receiver’s MAC address, public key, and previously computed key. Since the length of the parameters is consistent during this procedure, the time between each key does not vary much.

### Time to encrypt video chunks

This section has talked about how long it takes to encrypt each chunk. Although the video processing modules split the video file into chunks for each full frame, the implementation assumes the chunk size to be 1 MB. The video chunks are fed into the AES module before being transmitted. The chunks are mostly the same in that it varies between 1MB and 1.2MB, and the time taken to encrypt each also varies between 0.9 sec to 1.2 sec.

### Number of keys generated

The number of keys generated depends on the quantity of generated video chunks. This statistic has been considered for the study because the suggested solution uses multiple key technologies to provide improved security. Multiple keys have no impact on memory use because the keys are only momentarily saved at the transmitter and receiver sides. Furthermore, because each key is only utilized once, an increase in the number of keys has no impact on the fetching delay.

## Installing Entire Project

1. `git clone https://github.com/themj0ln1r/novel-cryptography-project.git`

2. `cd novel-cryptography-project`

3. python3 -m venv env

4. source env/bin/activate

5. pip3 install -r requirements.txt

Now you are set to run this project

- Move to Flask_App directory run the `app.py`

- Visit your localhost to view the webpage on action

- Register an account on the webpage

- Start the `server.py` and run the `client.py` 

- Input the required data in the `client.py` console

- Import your private to play the video 


**Keywords**: Hybrid Cryptography, Multikey Cryptography, Video Communication, Real-time Streaming, Elliptic Curve Cryptography (ECC), AES Encryption, Client-Server Model, Socket Programming, Flask, SQLAlchemy, RSA, Key Generation

### References

- Research paper published by [Sir. M. Ramakrishna](https://www.linkedin.com/in/rkmundugar/)
- Cryptography knowledge by [Prof.Christof paar](https://www.crypto-textbook.com/)
- Socket Programming tutorial by [Real Python](https://realpython.com/python-sockets/)
- Flask tutorial by [freecodecamp](https://www.youtube.com/watch?v=Z1RJmh_OqeA)

### Additional Links

For the full walk-through : [Blog](https://themj0ln1r.github.io/)