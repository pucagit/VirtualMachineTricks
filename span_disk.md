Here is the complete, step-by-step guide to expand your disk from start to finish.
## Step 1: Install the Growth Tool

```
sudo apt update && sudo apt install -y cloud-guest-utils
```

## Step 2: Turn Off and Delete Blocking Swap

```
sudo swapoff -a

(echo d; echo 5; echo d; echo 2; echo w) | sudo fdisk /dev/sda
```

## Step 3: Expand the Partition

```
sudo growpart /dev/sda 1
```

## Step 4: Expand the Filesystem

```
sudo resize2fs /dev/sda1
```

## Step 5: Verify the New Size

```
df -h /
```
