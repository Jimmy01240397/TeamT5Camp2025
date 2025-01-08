# Tpra exploit

Host OS: debian 12

## Emulate

1. Install binfmt tool and docker

```bash
sudo apt install qemu-user-binfmt binfmt-support binfmtc
```

2. Check binfmt

```bash
update-binfmts --display qemu-arm
```

3. Run `docker compose up -d`

4. To shell

```bash
docker compose exec firmware cbash 
```

## Exploit

```bash
python3 sr20_exploit.py 127.0.0.1 'echo pwned'
```

![image](https://github.com/user-attachments/assets/8778dff1-4c03-48be-b9f5-a50f2b5895b2)





