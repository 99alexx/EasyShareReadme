# Workflow from idea to finished product

EasyShare - Share files between friends quick and easy

The birth of the idea: When I was in university we sometimes worked in group projects. One recurring problem was to quickly and easily share files between each other, specifically 20MB+ sized files. 
I had bought an Rasperry Pi 5, and did not know what to really use it for...
So why not use the Pi to host a server and to build a relatively simple website to share files on. The upside of doing it this way is for me to learn along the way how to set up a server on a Pi, full controll of the server and management. 

To actually learn as much as possible I've tryed to limit the use of GenAI as much as possible.
Rules for usage:
  - Never copy code from the GenAI
  - First try to search for solutions on eg. Stackoverflow.
  - Have general informative discussions without code examples.

Tools/Frameworks etc:
- NodeJS, Express, Multer, prettier
- React/Vite, Tailwind

# The development plan (Implemented some improvements from Claude)

Phase 1: Basic Backend 
- Goal: Get file upload and download working
- Set up Express server
- Implement file upload endpoint
- Create temporary file storage on disk
- Build download endpoint with unique ID
- Test with tools like Postman/Thunder Client

Phase 2: Basic Frontend 
- Goal: Simple interface for testing functionality
- Create upload form
- Show generated link after upload
- Create download page that accepts link/ID
- Basic CSS/styling

Phase 3: Link Management & Security
- Goal: Secure, unique links
- Generate cryptographically secure IDs
- Implement link validation
- Add basic security headers
- File size and file type validation

- Used: Helmet, express-rate-limit on client side
- Should implement: ClamAV or cloud API checker for anti-virus

Phase 4: Automatic Deletion
- Goal: Files disappear after 10 min or upon download
- Timer-based deletion
- Deletion on download
- Regular cleanup job
- Database/file to track file status

Phase 5: User Experience
- Goal: Make it user-friendly
- Progress bars for upload/download
- Error handling and user messages
- Responsive design for mobile
- Loading states and feedback

Phase 6: Performance & Robustness
- Goal: Handle large files and multiple users
- Streaming for large files
- Rate limiting
- Proper error handling
- Memory management
- Cleanup code, project structure https://github.com/alan2207/bulletproof-react/blob/master/docs/project-structure.md

Phase 7: Production & Deployment
- Goal: Go live on Raspberry Pi
- Domain setup and DNS
- SSL certificate
- Nginx reverse proxy
- Process management (PM2)
- Monitoring and logs

# How it went

# Phase 1:
Was pretty straight forward. Setting up a simple express server with a couple of GET/POST endpoints. 
Implemented React, Vite dev tool, TailwindCSS framework and Multer. 
Choices:
I basically choose React/Vite/Tailwind because I wanted to explore and learn the industry standard frameworks and libraries, and how to make development faster.
Decided to use Multer library for it's simplicity, being able to store on disk.
I used Postman a bit in the beginning for calls to the API.
Unique ID I choose to go with UUIDV4 because it's easy to setup and implement + making it slim to zero chance of duplicates, although probably not necessary because the files are only on the disk for a very short time.

# Phase 2:
Spent a bit to much time on this step, since it was only supposed to be a simple "frame" with some functionallity. As seen in First draft below, that would probably been enough, but I continued and ended up with Second Draft. Which is a bit to much UI for this phase.

# Phase 3:
As from phase one I've already established to use uuidv4 to create secure unique links. So each file that is uploaded concists of (uuidv4 ID) + (name of file) + (filesize).
Used Helmet middleware to create basic security headers, since I feel it's "good enough" for this application.
I made a file checker function which checks so the file doesn't exceed 100MB, and file type validation. I only have size checker on the clientside, would probably be good to have it on the server aswell.
A concern I had was to probably check the files for malware before uploading them to the RaspberryPi, although they will never be opened on the disk. The two most promenent solutions is to use either ClamAV, a open-source malwvare program or a cloud API checker. Neither is implemented yet.

# Phase 4:
# Phase 5:
# Phase 6:

express-rate-limit

# Phase 7:

# UI Iteration
First draft
![first](imagesREADME/First.png)

Second draft
![second](imagesREADME/Second.png)

Third
![third](imagesREADME/Third.png)

Fourth (After test on users, I've added a info startpage for better UX)
![fourth](imagesREADME/Fourth.png)
