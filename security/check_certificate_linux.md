## Verifying FastTransfer Linux Binary Integrity and Authenticity

The zip file contains 3 files:
- `FastTransfer`
- `FastTransfer.sha256sum.txt`
- `FastTransfer.sha256sum.txt.asc`

To check the integrity of your `FastTransfer` file, generate its SHA256 sum and compare it with the sum present in `FastTransfer.sha256sum.txt`:

```bash
sha256sum -b FastTransfer
```

	d0e9b29b447da1e8aa946d0fcfe31a8e60d8411c5aad791439d3356e07ade907 *FastTransfer

```bash
cat FastTransfer.sha256sum.txt
```

	D0E9B29B447DA1E8AA946D0FCFE31A8E60D8411C5AAD791439D3356E07ADE907  FastTransfer%    

Or you can verify its integrity using a single command:
```bash
sha256sum -c FastTransfer.sha256sum.txt
```

	FastTransfer: OK

### Authenticity check

To verify the authenticity of `FastTransfer.sha256sum.txt`, check the signature of `FastTransfer.sha256sum.txt.asc` by following the steps below.

#### Download the FastTransfer signing key:

```bash
gpg --keyserver keys.openpgp.org --recv-keys 37007D091BF7DCC74D208A1F869511C7130465C8
```

	gpg: key 869511C7130465C8: "Francois Pacull <francois.pacull@architecture-performance.fr>" not changed
	gpg: Total number processed: 1
	gpg:              unchanged: 1

You can check that the key was properly imported:

```bash
gpg --list-key --with-fingerprint 130465C8
```

The output should contain 3700 7D09 1BF7 DCC7 4D20  8A1F 8695 11C7 1304 65C8 and look like this:

	pub   rsa4096 2025-04-11 [SC]
	      3700 7D09 1BF7 DCC7 4D20  8A1F 8695 11C7 1304 65C8
	uid           [ultimate] Francois Pacull <francois.pacull@architecture-performance.fr>
	sub   rsa4096 2025-04-11 [E]


#### Verify the authenticity of `FastTransfer.sha256sum.txt`

```bash
gpg --verify FastTransfer.sha256sum.txt.asc FastTransfer.sha256sum.txt
```
	gpg: Signature made Fri 11 Apr 2025 04:22:51 PM CEST
	gpg:                using RSA key 37007D091BF7DCC74D208A1F869511C7130465C8
	gpg: checking the trustdb
	gpg: marginals needed: 3  completes needed: 1  trust model: pgp
	gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
	gpg: Good signature from "Francois Pacull <francois.pacull@architecture-performance.fr>" [ultimate]

The output of the last command should tell you that the file signature is `good` and that it was signed with the 37007D091BF7DCC74D208A1F869511C7130465C8 key.

