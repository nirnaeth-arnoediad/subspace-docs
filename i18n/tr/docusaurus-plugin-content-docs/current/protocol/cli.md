---
title: Subspace CLI (Recommended)
sidebar_position: 2
description: Farming on the Subspace Network
keywords:
    - Farmer
    - Farming
    - CLI
    - Binaries
    - GitHub
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import Link from '@docusaurus/Link';
import styles from '@site/src/pages/index.module.css';

:::tip Tavsiye
[Subspace CLI](https://github.com/subspace/subspace-cli) Subspace Network'de çiftçilik yapmak için önerilen yoldur. Başlamak için aşağıdaki kılavuzu izleyin. Daha fazla bilgi için, projenin [GitHub README](https://github.com/subspace/subspace-cli/blob/main/README.md) kısmını ziyaret edebilirsiniz.
:::

## Ön Koşullar

---

### Sistem Gereksinimleri

:::danger Çiftçilik, Ağ Yoğunluğuna Sebep Olabilir.

Sabit bir ağ bağlantınız olduğundan emin olun. Çiftçiliğin parselleme aşaması sırasında, ağ yoğunluğu olabilir.

Bu, ağ kullanımınızı etkileyebilir, bu nedenle sabit bir veri sınırınız varsa lütfen ağ bağlantınızı kontrol edin.
:::

Subspace CLI'nin çalışması için emtia donanım özellikleri gerekir. **Minimum** olarak şunlara sahip olmanız önerilir:

| Donanım | Özellikler        |
| ------- | ----------------- |
| CPU     | 4 Core+           |
| RAM     | 4GB+ (Önrln. 8GB) |
| SWAP    | 4GB               |
| Storage | 50GB              |

:::note CoW Dosya Sistemleri Uyarısı
Herhangi bir işletim sistemi için CoW dosya sistemlerinde Subspace Çiftçi ve Düğümü'nün kullanılmaması tavsiye edilir.

BTRFS, Subspace ile birlikte kullanılıyorsa, Subspace başlatılmadan önce dizin/tüm dosya sistemi aşağıdaki komutla CoW devre dışı olarak ayarlanmalıdır.

**Cow Devre-dışı Bırakma Komutu**

```
sudo chattr +C veri/yolu
```

Alternatif olarak, bunun yerine ext4 veya xfs gibi CoW olmayan dosya sistemleri kullanılabilir.
:::

### Bir Kripto Cüzdanı Elde Etmek

Herhangi bir şeyi çalıştırmadan önce, testnet jetonlarını alacağınız bir cüzdanınız olması gerekir.
Cüzdan kurulumunuzu nasıl yapacağınıza ilişkin adımlar için dökümantasyonun [Cüzdanlar kategörisinde](/docs/category/wallets/) bulunan nasıl yapılır kılavuzlarımızı izleyin.

### Gerekli portlar

Şu anda, düğüm çalışmasının düzgün olması için birkaç bağlantı noktasının açılması gerekiyor.

Güvenlik duvarı olmayan bir sunucunuz varsa yapılacak bir şey yok, aksi takdirde gelen bağlantılar için aşağıdaki TCP portlarını açtığınızdan emin olun.

-   `30333`
-   `30433`

Masaüstü tarafında, bilgisayarınızın önünde bir yönlendiriciniz (modem) varsa, TCP bağlantı noktalarını düğümünüzün çalıştığı makineye yönlendirmeniz gerekir (bunun nasıl yapıldığı yönlendiriciden yönlendiriciye değişir, ancak her zaman böyle bir özellik vardır: bu konuda, daha ayrıntılı bir eğitim için [Bağlantı Noktaları Nasıl Yönlendirilir](port-forwarding.md) konusuna bakın).
Herhangi bir yönlendirici olmadan doğrudan bağlanırsanız, bu durumda yine hiçbir şey yapılmasına gerek yoktur.

## Kurulum

:::caution BAŞLANGIÇ YAZILIM
Subspace CLI **başlangıç** aşamasında.
Lütfen GitHub Issues kısmına ilgili hata raporları göndermekten çekinmeyin.
:::

### İkili Dosyaları İndirme

---

Subspace CLI'nin derlenmiş sürümleri [GitHub'da barındırılır](https://github.com/subspace/subspace-cli/releases). Uygulamayı yüklemek için önerilen yol budur. Lütfen işletim sisteminiz için uygun ikiliyi bulun.

<Tabs groupId="OS">

<TabItem value="windows" label="🖼️ Windows" default>

1. Aşağıdaki son sürüm ikili dosyasını indirin.

<div className={styles.buttons}>
    <Link
    className="button button--secondary button"
    to="https://github.com/subspace/subspace-cli/releases/download/v0.1.8-alpha/subspace-cli-windows-x86_64-v0.1.8-alpha.exe">
    ÇalıştırılabilirWindows CLI 
    </Link>
</div>

2. Powershell'i açın, `cd Yüklemeler` (veya `cd Sizin-Dosya-Konumunuz`) yazın.

</TabItem>

<TabItem value="macos" label="🍎macOS" default>

1. Aşağıdaki son sürüm ikili dosyasını indirin.

<div className={styles.buttons}>
    <Link
        className="button button--secondary button"
        to="https://github.com/subspace/subspace-cli/releases/download/v0.1.8-alpha/subspace-cli-macos-x86_64-v0.1.8-alpha.zip">
        Çalıştırılabilir Mac CLI (Intel)
    </Link>
    <Link
        className="button button--secondary button"
        to="https://github.com/subspace/subspace-cli/releases/download/v0.1.8-alpha/subspace-cli-macos-aarch64-v0.1.8-alpha.zip">
        Çalıştırılabilir Mac CLI (Apple M1)
    </Link>
</div>

2. `.zip` dosyasını ayıklayın.
3. Terminal'i açın, `cd Yüklemeler` (veya `cd Sizin-Dosya-Konumunuz`) yazın.
4. Aşağıdaki kod ile ikili dosyayı çalıştırılabilir yapın:
    - `chmod +x subspace-cli-macos-x86_64-v0.1.8-alpha` (Intel Chip)
    - `chmod +x subspace-cli-macos-aarch64-v0.1.8-alpha` (Apple M1 Chip)

</TabItem>
<TabItem value="linux" label="🐧Ubuntu">

1. Aşağıdaki son sürüm ikili dosyasını indirin.

<div className={styles.buttons}>
    <Link
        className="button button--secondary button"
        to="https://github.com/subspace/subspace-cli/releases/download/v0.1.8-alpha/subspace-cli-Ubuntu-x86_64-v0.1.8-alpha">
        Çalıştırılabilir Ubuntu
    </Link>
    <Link
        className="button button--secondary button"
        to="https://github.com/subspace/subspace-cli/releases/download/v0.1.8-alpha/subspace-cli-ubuntu-aarch64-v0.1.8-alpha">
        Çalıştırılabilir Linux Arch
    </Link>
</div>

2. Terminal'i açın, `cd Yüklemeler` (veya `cd Sizin-Dosya-Konumunuz`) yazın.
3. Aşağıdaki kod ile ikili dosyayı çalıştırılabilir yapın:
    - `chmod +x subspace-cli-ubuntu-x86_64-v0.1.8-alpha` (Ubuntu)
    - `chmod +x subspace-cli-ubuntu-aarch64-v0.1.8-alpha` (Linux Arch)

</TabItem>

</Tabs>

### Konfigürasyon

---

Başlamak için Çiftçimizi başlatmamız gerekecek, bu şu şekilde yapılabilir:

<Tabs groupId="OS">
<TabItem value="windows" label="🖼️ Windows" default>

```powershell
./subspace-cli-windows-x86_64-v0.1.8-alpha.exe init
```

</TabItem>

<TabItem value="macos" label="🍎 macOS">
Intel Chip:

```bash
subspace-cli-macos-x86_64-v0.1.8-alpha init
```

Apple M1 Chip:

```bash
subspace-cli-macos-aarch64-v0.1.8-alpha init
```

</TabItem>

<TabItem value="linux" label="🐧 Ubuntu">
Ubuntu:

```bash
subspace-cli-ubuntu-x86_64-v0.1.8-alpha init
```

Linux Arch:

```bash
subspace-cli-ubuntu-aarch64-v0.1.8-alpha init
```

</TabItem>
</Tabs>

This will prompt you to setup your CLI configurations to begin farming. You should see a similar prompt like so:

```bash
$ ./subspace-cli-ubuntu-x86_64-v0.1.8-alpha init

version: 0.1.0

SUBSPACE NETWORK

Configuration creation process has started...
Enter your farmer/reward address: REDACTED_ADDRESS
Enter your node name to be identified on the network(defaults to `username`, press enter to use the default):
Specify a plot location (press enter to use the default: `"/home/username/.local/share/subspace-cli/plots"`):
Specify a plot size (defaults to `1000.0 MB`, press enter to use the default):
Specify the chain to farm(defaults to `gemini-3c`, press enter to use the default):
Configuration has been generated at /home/username/.config/subspace-cli
Ready for lift-off! Run the following command to begin:
`./subspace-cli farm`
```

:::info Finding your settings.toml

After running `subspace-cli init`, the prompt will display where the `settings.toml` is generated. However in case you missed it, you can find the file based on your operating system:

<Tabs groupId="OS">
<TabItem value="windows" label="🖼️ Windows" default>

Your `settings.toml` will be found in `$FOLDERID_RoamingAppData/subspace-cli/settings.toml`

</TabItem>

<TabItem value="macos" label="🍎macOS">

Your `settings.toml` will be found in `$HOME/Library/Application Support/subspace-cli/settings.toml`

</TabItem>

<TabItem value="linux" label="🐧Ubuntu">

Your `settings.toml` will be found in `$HOME/.config/subspace-cli/settings.toml`

</TabItem>
</Tabs>

:::

### Gemini 3 Testnet

---

:::tip Use the default generated configuration!
The default configuration generated by Subspace CLI will have you ready for Gemini 3.
:::

If you are using the default configurations from Subspace CLI, you are ready to go with the Gemini 3 Testnet. Alternatively, you can ensure this occurs by manually setting the network like so.

Open your `settings.toml` directory and ensure your `chain` is correctly specified to `gemini-3c` as so:

```toml
# settings.toml
[node]
chain = 'gemini-3c'
# ... redacted ...
```

### Local Development

---

To run Subspace CLI in a local development mode, modify your `settings.toml` and ensure your `chain` points to `dev`:

```toml
# settings.toml
[node]
chain = 'dev'
# ... redacted ...
```

## Farming

---

To begin farming on the network, just run the `farm` command with the CLI like so:

<Tabs groupId="OS">
<TabItem value="windows" label="🖼️ Windows" default>

```powershell
./subspace-cli-windows-x86_64-v0.1.8-alpha.exe farm
```

</TabItem>

<TabItem value="macos" label="🍎 macOS">

Intel Chip:

```bash
subspace-cli-macos-x86_64-v0.1.8-alpha farm
```

Apple M1 Chip:

```bash
subspace-cli-macos-aarch64-v0.1.8-alpha farm
```

</TabItem>

<TabItem value="linux" label="🐧 Ubuntu">

Ubuntu:

```bash
subspace-cli-ubuntu-x86_64-v0.1.8-alpha farm
```

Linux Arch:

```bash
subspace-cli-ubuntu-aarch64-v0.1.8-alpha farm
```

</TabItem>
</Tabs>

You should see the farmer and node start successfully and begin syncing, plotting, and then farming:

```bash
$ ./subspace-cli-ubuntu-x86_64-v0.1.8-alpha farm
Starting node ... (this might take up to couple of minutes)
Node started successfully!
Starting farmer ...
Farmer started successfully!
Initial plotting for plot: #0 (/home/username/.local/share/subspace-cli/plots)
⠁ [00:00:00] 3% [=>                                      ]
      (31.00 MiB/953.67 MiB) 157.35 GiB/s, plotting, ETA: 0s
```

That's it! Enjoy and Happy Farming!

#### Moving the Farming Process to the Background

<Tabs groupId="OS">
<TabItem value="tmux" label="Tmux" default>

:::tip Learn More about Tmux

If you would like to learn more about Tmux and its options check out their Repo [here](https://github.com/tmux/tmux/wiki)

:::

-   Create a new tmux session using a socket file named farming

```bash
$ tmux -S farming
```

-   Move process to background by detaching

```bash
Ctrl+b d OR ⌘+b d (Mac)
```

-   To re-attach

```bash
$ tmux -S farming attach
```

-   To delete farming session

```bash
$ tmux kill-session -t farming
```

</TabItem>
<TabItem value="screen" label="Screen">

:::tip Learn More about Screen

If you would like to learn more about Screen and its options check out their Webpage [here](https://www.gnu.org/software/screen/)

:::

-   Create new screen using a socket file named farming

```bash
$ screen -S farming
```

-   Move process to background by detaching

```bash
Ctrl+d a OR ⌘+d a (Mac)
```

-   To re-attach

```bash
$ screen -r farming
```

-   To delete farming session

```bash
$ screen -S farming -X quit
```

</TabItem>
</Tabs>
