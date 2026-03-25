---
title: "Change Docker path (when Docker storage is insufficient)"
last_modified_at: 2026-03-25
categories:
    - Infra
---

> When developing with Docker, you may encounter issues where execution fails or processes stop due to insufficient storage. In such cases, you need to change to a path with sufficient capacity.

<br>

#### Clean up stopped containers, networks, images, etc.

Before changing the path, clean up unused resources first, as the storage shortage may be caused by them. 

```python
docker system prune
```

<br>

#### Check storage

The current root directory is about 89% full, and even after cleaning up unused resources, the storage is still insufficient. Changing the Docker path is necessary.

```python
df -h
```

![image](/assets/images/2/2-1.png)

<br>

#### Check the current path

{% raw %}
```python
docker info -f '{{ .DockerRootDir }}'
```
{% endraw %}

![image](/assets/images/2/2-2.png)

<br>

#### Stop the Docker service

If Docker is still running during the move, data loss or corruption may occur, so you must stop the Docker service first. 

```python
sudo systemctl stop docker
sudo systemctl stop docker.socket
```

<br>

#### Move existing data (current path → new path)

Move the data from the current path you checked earlier to the new path. 

```python
sudo mv /var/lib/docker /data
```

![image](/assets/images/2/2-3.png)

→ you can verify that the data was moved successfully using the `ls` command. 

<br>

#### Set the path

After moving the file, you need to inform Docker of the new path. Specify the new root path in the `daemon.json` file.

```python
sudo vi /etc/docker/daemon.json
```

```python
{
  "data-root": "/data"
}
```

<br>

#### Restart

```python
sudo systemctl start docker
```

<br>

#### Check the new path

{% raw %}
```python
docker info -f '{{ .DockerRootDir }}'
```
{% endraw %}

![image](/assets/images/2/2-4.png)

→ You can verify that the data has been successfully moved to the `/data` folder.

<br>
<br>
