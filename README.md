# Dockerfile Bug: Missing Working Directory

This repository demonstrates a common error in Dockerfiles:  failure to set a working directory.  The provided `Dockerfile` uses the minimal `alpine` image and installs Python dependencies correctly, but the `CMD` instruction fails because the application's entrypoint (`main.py`) is not located in a known directory.

## Bug

The bug lies in the absence of a `WORKDIR` instruction before the `CMD`. Without this, the application will attempt to run from the root directory of the container, which likely doesn't contain the `main.py` file.

## Solution

The `DockerfileSolution.txt` provides the corrected `Dockerfile`, including a `WORKDIR` instruction to ensure the application runs correctly.

## Running the Example

1. Clone the repository.
2. Build the original (buggy) image: `docker build -f Dockerfile -t buggy-app .`
3. Attempt to run the buggy image (it will likely fail): `docker run buggy-app`
4. Build the corrected image: `docker build -f DockerfileSolution.txt -t fixed-app .`
5. Run the corrected image (it should succeed if `main.py` is correctly placed): `docker run fixed-app`