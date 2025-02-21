import docker
import os

# Initialize Docker client
client = docker.from_env()

def build_docker_image(dockerfile_path, image_tag):
    """Builds a Docker image from the specified Dockerfile."""
    try:
        print(f"Building Docker image with tag: {image_tag}...")
        image, build_logs = client.images.build(path=dockerfile_path, tag=image_tag)
        
        # Print build logs
        for log in build_logs:
            if 'stream' in log:
                print(log['stream'].strip())
        
        print(f"Image {image_tag} built successfully!")
    except docker.errors.BuildError as build_error:
        print(f"Error building image: {build_error}")
    except Exception as e:
        print(f"Unexpected error: {e}")

def run_docker_container(image_tag):
    """Runs a Docker container from the built image."""
    try:
        print(f"Running container from image: {image_tag}...")
        container = client.containers.run(image_tag, detach=True)
        print(f"Container {container.short_id} is running...")
        return container
    except docker.errors.ImageNotFound:
        print(f"Error: Image {image_tag} not found!")
    except Exception as e:
        print(f"Unexpected error: {e}")

def stop_docker_container(container):
    """Stops a running container."""
    try:
        print(f"Stopping container {container.short_id}...")
        container.stop()
        print(f"Container {container.short_id} stopped successfully!")
    except Exception as e:
        print(f"Error stopping container: {e}")

if __name__ == "__main__":
    dockerfile_path = "."  # Path to directory containing Dockerfile (default is current directory)
    image_tag = "myapp:latest"  # Name and tag for the Docker image

    # Build Docker image
    build_docker_image(dockerfile_path, image_tag)
    
    # Run Docker container
    container = run_docker_container(image_tag)
    
    # Stop container after some time (for demonstration purposes)
    input("Press Enter to stop the container...")
    stop_docker_container(container)
