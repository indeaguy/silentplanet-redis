# SilentPlanet Redis Configuration

This guide describes how to include the silent-planet Redis configuration file (`redis.bagel.conf`) into your existing `redis.conf` file and how to test the new configurations.

## Files

- `redis.conf`: Your existing Redis configuration file.
- `redis.bagel.conf`: The new configuration file in this repo that contains additional settings.

## Steps to Include and Test the Configuration

### 1. Update Your Existing `redis.conf` File

Add the following line at the end of your existing `redis.conf` file to include the `redis.bagel.conf` file:

```sh
# Include additional configuration
include /absolute/path/to/redis.bagel.conf
```

Replace `/absolute/path/to/redis.bagel.conf` with the actual path to your `redis.bagel.conf` file.

### 2. Restart Redis

Restart the Redis service to apply the new configuration:

#### Using homebrew

```sh
brew services restart redis
```

### 3. Verify the New Configuration

Use `redis-cli` to check that the new configurations have been applied:

```sh
redis-cli CONFIG GET appendonly
redis-cli CONFIG GET appendfilename
redis-cli CONFIG GET appendfsync
redis-cli CONFIG GET save
```

### Expected Output

The expected output should reflect the settings from `redis.bagel.conf`:

```
1) "appendonly"
2) "yes"
1) "appendfilename"
2) "appendonly.aof"
1) "appendfsync"
2) "everysec"
1) "save"
2) "900 1"
3) "300 10"
4) "60 10000"
```