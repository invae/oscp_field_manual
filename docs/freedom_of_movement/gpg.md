# gpg

## gen burner keypair

```bash
gpg --generate-key
```
- answer questions accordingly

## export key as pem

```bash
gpg --armor  --export-secret-keys example@email.com > identity.key
```

## export pub as pem

```bash
gpg --armor  --export example@email.com > identity.key.pub
```

## encrypt a message

```bash
gpg --armor -r recipient@email.com -e message.txt
```

## decrypt with our pubkey

```bash
gpg -d tmp.txt.gpg 
```
- you will be prompted for the pass associated with the burner

## verify signed message

```bash
gpg --status-fd 1 --verify example.signed  
```

## sign a message

```bash
gpg -a  -s --default-key <KEY_SLUG_FOR_SIGN> message.txt
```

