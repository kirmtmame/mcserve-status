# MinecraftServerPinger

A lightweight Java library to fetch the status of any Java Edition Minecraft server, without dealing with raw ping or protocol details.

## Features ✅

Check if a server is online/offline

Get server version and protocol

Get online player count and sample list

Protocol fallback detection

Full error handling

### Installation

- Maven

```bash
<dependency>
  <groupId>net.xpcraft</groupId>
  <artifactId>minecraftserverpinger</artifactId>
  <version>1.0.0</version>
</dependency> 
```

- Gradle

``` bash
implementation 'net.xpcraft:minecraftserverpinger:1.0.0'
```
---

**Usage**

``` bash
import net.xpcraft.status.client.MinecraftServerPinger;
import net.xpcraft.status.model.ServerStatus;

public class Main {
    public static void main(String[] args) {
        MinecraftServerPinger pinger = new MinecraftServerPinger("play.hypixel.net", 25565);
        ServerStatus status = pinger.ping();

        if (status.isOnline()) {
            System.out.println("✅ Server is online!");
            System.out.println("Version: " + status.getVersion().getNameClean() +
                               " (Protocol: " + status.getVersion().getProtocol() + ")");
            System.out.println("Players: " + status.getPlayers().getOnline() + "/" +
                               status.getPlayers().getMax());
            System.out.println("MOTD:\n" + status.getMotd());
        } else {
            System.out.println("❌ Server is offline");
            if (status.getErrorMessage() != null)
                System.out.println("Error: " + status.getErrorMessage());
        }
    }
}
```

---

- **Notes**

Protocol: The library first attempts to fetch the protocol via ProtocolFetcher; if unavailable, it uses ProtocolDetector.

Fallback: If the server is offline or unreachable, ServerStatus.isOnline() will be false and the error details are stored in ServerStatus.getErrorMessage().

We will publish the project source soon.

--- 

- **Author**

Created By XpCraftTeam

---

- SocialMedia

[InstaGram](https://www.instagram.com/meme.traker?igsh=MTZhc2R2MXJoZHAyZg==)

[Telegram](https://t.me/meme_mrtraker)
