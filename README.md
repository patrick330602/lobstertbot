# LobsterTBot

LobsterTBot (Short for **L**inode **Ob**ject **St**orage-C**ertbot** hook scripts) is a easy way to setup SSL for custom domain using Certbot for your Linode Object Storage Buckets.

## The (Sad) Story

```
Me: *Sets up a Linode Object Storage*
    *Copy files over from old OSS*
    *Found out you have to use the custom domain name for your OS for SSL Certificate to work*
    *Delete old one and create a correct one*
    *copy file and Cyberduck won't stop qucking error*
    *finally*
    *Trying to set up ACME Challege using Certbot*
    *domain points to old OS randomly, ACME Challenge failed*
    *re-setup old OS, finally works*
    *certbot renew command complains about no hook*
    *lie down*
    *try not to cry*
    *cry a lot*
    *wrote these scripts for automatic hook*
```

## Prerquirements
- [An Linode Object Storage Bucket](https://www.linode.com/docs/guides/enable-ssl-for-object-storage/#create-an-object-storage-bucket)
forthe domain with same name as DNS.
- [A DNS](https://www.linode.com/docs/guides/enable-ssl-for-object-storage/#configure-dns) pointed to the bucket.
- A Linode [Personal Access Token](https://cloud.linode.com/profile/tokens)
with Read/Write permission to Object Storage.
- `certbot` installed using `snap`or other method; `snap` version will come with an automatic renewer.
- `python3` installed. Just Python3 is good enough.

## Usage

- Clone the repository using `root` account;
- Fill the detailed information in `secrets`;
- Edit `auth` and `clean` and change `source /<path>/secrets` to the actual path to `secrets`;
- Execute the following using `root`:
```bash
certbot certonly -d <custom-domain> --manual --preferred-challenges http --manual-public-ip-logging-ok --manual-auth-hook $(pwd)/auth --manual-cleanup-hook $(pwd)/clean
```
  Where custom domain is your desired domain you want to use with the bucket;
- Annnnd you are done.

## License

MIT.





