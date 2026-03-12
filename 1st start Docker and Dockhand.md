The Complete Docker Desktop & Dockhand Starter Manual
What are Docker and Dockhand? (The 10-Year-Old Explanation)
Imagine you have a giant lunchbox with perfect, sealed compartments.

Docker is the lunchbox. It holds all your different snacks (software apps) in their own sealed compartments (called containers). Your sandwich never gets soggy from your juice because they are perfectly separated, but they still travel together in the same box.

Dockhand is the clear lid on top of the lunchbox. Instead of blindly reaching in and guessing what snack you are grabbing, Dockhand lets you look inside, see exactly what is running, and organize everything with simple clicks.

Step 1: Setting Up Docker Desktop
This is the engine that runs everything. We need to install this foundation first.

Download: Go to the official Docker website and download Docker Desktop for your specific operating system (Windows, Mac, or Linux).

Install: Run the downloaded file. If you are on Windows, ensure the option for "WSL 2" is checked during installation, as this allows the engine to run much faster.

Start: Open the Docker Desktop application. It will run quietly in the background. You will see a small whale icon in your system tray indicating the engine is running and ready.

Step 2: Setting Up Dockhand for Web Management
Instead of typing long, confusing commands into a terminal to control your containers, we will install Dockhand. It is the absolute best-suited visual dashboard right now—it is fast, self-hosted, and handles complex deployments effortlessly.

We will use a single configuration file to tell Docker exactly how to build it.

Create a new folder on your computer called dockhand_setup.

Inside that folder, create a plain text file and name it exactly docker-compose.yml.

Paste the following clean, commented code into that file:

YAML
# dockhand application service
services:
  dockhand:
    image: fnsys/dockhand:latest
    container_name: dockhand
    restart: unless-stopped
    ports:
      # maps port 3000 on your computer to port 3000 in the container
      - 3000:3000
    volumes:
      # allows dockhand to talk directly to the docker engine
      - /var/run/docker.sock:/var/run/docker.sock
      # saves your configurations and data persistently
      - dockhand_data:/app/data

# defines the persistent storage volume
volumes:
  dockhand_data:
Run it: Open your computer's terminal (or command prompt), navigate to the dockhand_setup folder you just created, and execute this command:
docker compose up -d

Access the Dashboard: Open your web browser and navigate to http://localhost:3000. You will be greeted by the Dockhand setup screen to create your initial admin account.

Step 3: A Small Guide to Using Dockhand
Once logged in, here is how you navigate and manage your environment:

Dashboard: This is your home base. It gives you a real-time, visual breakdown of how much CPU and memory your active containers are consuming.

Containers Tab: Click this to see every app you have running. You will find simple buttons to "Start", "Stop", and "Restart" next to each container. Clicking on a specific container allows you to read its live logs (to see what the app is doing behind the scenes) or open an interactive web terminal without needing SSH.

Stacks Tab: When you want to add complex apps that require multiple containers (like a web server paired with a database), you use Stacks. You can write or paste a docker-compose.yml file directly into the visual editor here, and Dockhand will spin up the entire environment automatically.

Volumes & Images: Think of Images as the blueprints for your apps, and Volumes as the hard drives where they save their data. You can click these tabs to browse your files directly through the web interface or cleanly delete old blueprints you no longer need to free up space.
