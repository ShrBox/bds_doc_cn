> [bds_doc_cn](http://github.com/ShrBox/bds_doc_cn) by [ShrBox](http://github.com/ShrBox)
# **如何使用基岩版专用服务器**

## **免责声明**

这是我们尚未完全支持的早期alpha版本，它可能存在严重的问题，我们会随时停止支持。

## **推荐配置**

我们推荐在至少拥有两个核心和1Gb内存的64位Intel或AMD处理器的服务器上运行基岩版专用服务器。

## **平台**

### **Linux**

Linux版本的基岩版专用服务器需要Ubuntu 18及以上的版本，不支持除Ubuntu外其它的发行版
解压压缩文件到一个空的文件夹。输入以下命令启动服务器：

`LD_LIBRARY_PATH=. ./bedrock_server`

### **Windows**

Windows版的基岩版专用服务器需要:

- Windows 10 1703及以上版本
- Windows Server 2016及以上版本
解压压缩文件到一个空的文件夹。执行 `bedrock_server.exe` 文件来启动服务器

在某些系统上，当您希望连接到本地计算机运行的服务器上时
您需要解除Minecraft客户端的UWP loopback限制，请输入以下命令: 
`CheckNetIsolation.exe LoopbackExempt –a –p=S-1-15-2-1958404141-86561845-1752920682-3514627264-368642714-62675701-733520436`

## **配置文件**

服务器将会尝试读取一个名为 `server.properties` 的文件。当一个世界被创建后某些选项是只读的，而另一些则在每次启动时读取。该文件内有一些配置项，其中的键和值以等号分隔，每行一个。

以下选项是可用的。如果括号中的值为数字，则可以使用该数字代替文本值。

<table>
    <thead>
        <tr>
            <th>选项</th>
            <th>可用值</th>
            <th>默认值</th>
            <th>被使用的时候</th>
            <th>注意</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>gamemode</td>
            <td>survival (0), creative (1), adventure (2)</td>
            <td>survival</td>
            <td>始终或仅针对新玩家</td>
            <td>游戏模式，其中survival为生存，creative为创造，adventure为冒险</td>
        </tr>
        <tr>
            <td>difficulty</td>
            <td>peaceful (0), easy (1), normal (2), hard (3)</td>
            <td>easy</td>
            <td>始终</td>
            <td>难度，peaceful为和平，easy为简单，normal为普通，hard为困难</td>
        </tr>
        <tr>
            <td>level-type</td>
            <td>FLAT, LEGACY, DEFAULT</td>
            <td>DEFAULT</td>
            <td>世界被创建时</td>
            <td>世界类型，FLAT为超平坦，LEGACY为有限世界，DEFAULT为无限世界</td>
        </tr>
        <tr>
            <td>server-name</td>
            <td>任何字符串</td>
            <td>Dedicated Server</td>
            <td>始终</td>
            <td>这是服务器的名称，会在游戏中的服务器列表中显示</td>
        </tr>
        <tr>
            <td>max-players</td>
            <td>任何整数</td>
            <td>10</td>
            <td>始终</td>
            <td>服务器最多可加入玩家的数量。<b>较高的值会对性能产生影响</b></td>
        </tr>
        <tr>
            <td>server-port</td>
            <td>任何整数</td>
            <td>19132</td>
            <td>始终</td>
            <td>服务器端口</td>
        </tr>
        <tr>
            <td>server-portv6</td>
            <td>任何整数</td>
            <td>19133</td>
            <td>始终</td>
            <td>服务器IPV6端口</td>
        </tr>
        <tr>
            <td>level-name</td>
            <td>任何字符串</td>
            <td>level</td>
            <td>始终</td>
            <td>被使用/创建的世界的名字。每个世界都在`/worlds`中有自己的文件夹</td>
        </tr>
        <tr>
            <td>level-seed</td>
            <td>任何字符串 </td>
            <td></td>
            <td>世界被创建时</td>
            <td>用于生成世界的种子，如果为空则随机生成种子</td>
        </tr>
        <tr>
            <td>online-mode</td>
            <td>true, false</td>
            <td>true</td>
            <td>始终</td>
            <td>如果为true则所有连接的玩家必须登录微软账户
                无论此设置项如何，连接到远程（非局域网）服务器的客户端始终需要登录微软账户。
                如果服务器接受来自互联网的连接（开放给所有玩家游玩），我们<b>非常</b>推荐打开online-mode</td>
        </tr>
        <tr>
            <td>white-list</td>
            <td>true, false</td>
            <td>false</td>
            <td>始终</td>
            <td>如果值为true则所有连接的玩家必须存在于<code>whitelist.json</code>文件中
                请参考<a href="#白名单">部分</td>
        </tr>
        <tr>
            <td>allow-cheats</td>
            <td>true, false</td>
            <td>false</td>
            <td>始终</td>
            <td>是否允许使用作弊命令，打开此项将无法获得成就</td>
        </tr>
        <tr>
            <td>view-distance</td>
            <td>任何整数</td>
            <td>10</td>
            <td>始终</td>
            <td>玩家最远可以看到的距离，<b>请根据服务器性能调整</b>。因为客户端最大视距为32个区块，所以就算将此项改成114514效果也等同于32。</td>
        </tr>
        <tr>
            <td>player-idle-timeout</td>
            <td>任何整数</td>
            <td>30</td>
            <td>始终</td>
            <td>玩家不移动多少分钟后将会被踢出服务器。如果设置为0则禁用此功能</td>
        </tr>
        <tr>
            <td>max-threads</td>
            <td>任何整数</td>
            <td>8</td>
            <td>设置</td>
            <td>服务器可以使用的最大线程数</td>
        </tr>
        <tr>
            <td>tick-distance</td>
            <td>4-12的整数</td>
            <td>4</td>
            <td>始终</td>
            <td>玩家周围多少个区块将会被更新，请根据服务器性能调整</td>
        </tr>
        <tr>
            <td>default-player-permission-level</td>
            <td>visitor, member, operator</td>
            <td>member</td>
            <td>始终</td>
            <td>当玩家第一次加入服务器时默认的权限等级，visitor为访客，member为成员，operator为OP</td>
        </tr>
        <tr>
            <td>texturepack-required</td>
            <td>true, false</td>
            <td>false</td>
            <td>始终</td>
            <td>强制客户端使用服务器加载的材质包</td>
        </tr>
        <tr>
            <td>content-log-file-enabled</td>
            <td>true, false</td>
            <td>false</td>
            <td>始终</td>
            <td>是否将内容错误记录到文件中。</td>
        </tr>
        <tr>
            <td>compression-threshold</td>
            <td>0-65535的整数</td>
            <td>1</td>
            <td>始终</td>
            <td>压缩的原始网络负载的最小大小，可用于实验CPU带宽权衡</td>
        </tr>
        <tr>
            <td>server-authoritative-movement</td>
            <td>true, false</td>
            <td>true</td>
            <td>始终</td>
            <td>玩家移动检测。如果为true，服务器将会重放玩家的移动行为，并在客户端位置于服务器位置不匹配时更正</td>
        </tr>
        <tr>
            <td>player-movement-score-threshold</td>
            <td>任何正整数</td>
            <td>20</td>
            <td>始终</td>
            <td>报告异常行为之前所需的不一致时间间隔的数量。
            换句话说，就是在服务器更正玩家位置之前，玩家的位置错误达到了几次，服务器才会进行更正。
            仅与<code>server-authoritative-movement</code>相关</td>
        </tr>
        <tr>
            <td>player-movement-distance-threshold</td>
            <td>任何正浮点数</td>
            <td>0.3</td>
            <td>始终</td>
            <td>如果服务器位置与客户端位置之间的差异超过了此数，服务器将会更正玩家的位置。
            仅与<code>server-authoritative-movement</code>相关</td>
        </tr>
        <tr>
            <td>player-movement-duration-threshold-in-ms</td>
            <td>任何正整数</td>
            <td>500</td>
            <td>始终</td>
            <td>在异常移动次数增加之前，服务器和客户端位置可能不同步的持续时间（由<code>player-movement-distance-threshold</code>定义）。以毫秒为单位
            仅与<code>server-authoritative-movement</code>相关</td>
        </tr>
        <tr>
            <td>correct-player-movement</td>
            <td>true, false</td>
            <td>false</td>
            <td>始终</td>
            <td>如果为true，当客户端异常移动次数超过了阈值，服务器将更正客户端位置
                仅与<code>server-authoritative-movement</code>相关</td>
        </tr>
    </tbody>
</table>

## **文件夹**

当解压时你会看到一些文件夹和可执行文件。
当服务器启动时将会创建一堆空文件夹。
您应该关注如下文件夹:

<table>
    <thead>
        <tr>
            <th>文件夹名e</th>
            <th>用途</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>behavior_packs</td>
            <td>在这里可以安装新的行为包。目前尚无法在一个世界中激活它们。</td>
        </tr>
        <tr>
            <td>resource_packs</td>
            <td>在这里可以安装新的材质包。目前尚无法在一个世界中激活它们。</td>
        </tr>
        <tr>
            <td>worlds</td>
            <td>如果这个文件夹不存在，则会在服务器启动时创建。Every world created will have a
                folder named according to their `level-name` inside the `server.properties` file.</td>
        </tr>
    </tbody>
</table>

## **Whitelist**

If the `white-list` property is enabled in `server.properties` then the server will only allow selected users to connect. To allow a user to connect you need to know their Xbox Live Gamertag. The easiest way to add a user to the whitelist is to use the command `whitelist add "Gamertag"` (eg: `whitelist add ExampleName`). Note: If there is a white-space in the Gamertag you need to enclose it with double quotes: `whitelist add "Example Name"`

If you later want to remove someone from the list you can use the command `whitelist remove "Gamertag"`.

The whitelist will be saved in a file called `whitelist.json`. If you want to automate the process of adding or removing players from it you can do so. After you've modified the file you need to run the command `whitelist reload` to make sure that the server knows about your new change.

The file contains a JSON array with objects that contains the following key/values.

<table>
    <thead>
        <tr>
            <th>Key</th>
            <th>Type</th>
            <th>Value</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>name</td>
            <td>String</td>
            <td>The gamertag of the user.</td>
        </tr>
        <tr>
            <td>xuid</td>
            <td>String</td>
            <td>Optional. The XUID of the user. If it's not set then it will be populated when someone with a matching
                name connects.</td>
        </tr>
        <tr>
            <td>ignoresPlayerLimit</td>
            <td>Boolean</td>
            <td>True if this user should not count towards the maximum player limit. Currently there's another soft
                limit of 30 (or 1 higher than the specified number of max players) connected players, even if players
                use this option. The intention for this is to have some players be able to join even if the server is
                full.</td>
        </tr>
    </tbody>
</table>

Example `whitelist.json` file:

```
[
{
    "ignoresPlayerLimit": false,
    "name": "MyPlayer"
},
{
    "ignoresPlayerLimit": false,
    "name": "AnotherPlayer",
    "xuid": "274817248"
}
]
```

## **权限**

You can adjust player specific permissions by assigning them roles in the `permissions.json` that is placed in the same directory as the server executable. The file contains a simple JSON object with XUIDs and permissions. Valid permissions are: `operator`, `member`, `visitor`. Every player that connects with these accounts will be treated according to the set premission. If you change this file while the server is running, then run the command `permissions reload` to make sure that the server knows about your new change. You could also list the current permissions with `permissions list`. Note that `online-mode` needs to be enabled for this feature to work since xuid requires online verification of the user account. If a new player that is not in this list connects, the `default-player-permission-level` option will apply.

Example `permissions.json` file:

```
[
    {
        "permission": "operator",
        "xuid": "451298348"
    },
    {
        "permission": "member",
        "xuid": "52819329"
    },
    {
        "permission": "visitor",
        "xuid": "234114123"
    }
]<
```

## **崩溃报告**

If the server crashes it will automatically send us various information that helps us solve it for the future.

## **命令**

You can issue commands to the server by typing in the console. The following commands are available. &lt; &gt; means a parameter is required, [ ] means it's optional and | denotes different allowed values. Strings can be enclosed in double quotes, ", if they contain spaces.

<table>
    <thead>
        <tr>
            <th>Command syntax</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>kick &lt;player name or xuid&gt; &lt;reason&gt;</td>
            <td>Immediately kicks a player. The reason will be shown on the kicked players screen.</td>
        </tr>
        <tr>
            <td>stop</td>
            <td>Shuts down the server gracefully.</td>
        </tr>
        <tr>
            <td>save &lt;hold | resume | query&gt;</td>
            <td>Used to make atomic backups while the server is running. See the backup section for more information.
            </td>
        </tr>
        <tr>
            <td>whitelist &lt;on | off | list | reload&gt;</td>
            <td>
                `on` and `off` turns the whitelist on and off. Note that this does not change the value in the
                `server.properties` file!</br></br>
                `list` prints the current whitelist used by the server</br></br>
                `reload` makes the server reload the whitelist from the file.</br></br>
                See the Whitelist section for more information.
            </td>
        </tr>
        <tr>
            <td>whitelist &lt;add | remove&gt; &lt;name&gt;</td>
            <td>Adds or removes a player from the whitelist file. The name parameter should be the Xbox Gamertag of the
                player you want to add or remove. You don't need to specify a XUID here, it will be resolved the first
                time the player connects.</br></br>
                See the Whitelist section for more information.</td>
        </tr>
        <tr>
            <td>permission &lt;list | reload&gt;</td>
            <td>
                `list` prints the current used operator list.</br></br>
                `reload` makes the server reload the operator list from the ops file.</br></br>
                See the Permissions section for more information.
            </td>
        </tr>
        <tr>
            <td>op &lt;player&gt;</td>
            <td>
                Promote a player to `operator`. This will also persist in `permissions.json` if the player is
                authenticated to XBL. If `permissions.json` is missing it will be created. If the player is not
                connected to XBL, the player is promoted for the current server session and it will not be persisted on
                disk. Defualt server permission level will be assigned to the player after a server restart.
            </td>
        </tr>
        <tr>
            <td>deop &lt;player&gt;</td>
            <td>
                Demote a player to `member`. This will also persist in `permissions.json` if the player is authenticated
                to XBL. If `permissions.json` is missing it will be created.
            </td>
        </tr>
        <tr>
            <td>changesetting &lt;setting&gt; &lt;value&gt;</td>
            <td>Changes a server setting without having to restart the server. Currently only two settings are supported
                to be changed, `allow-cheats` (true or false) and `difficulty` (0, `peaceful`, 1, `easy`, 2, `normal`, 3
                or `hard`). They do not modify the value that's specified in `server.properties`.</td>
        </tr>
    </tbody>
</table>

## **备份**

The server supports taking backups of the world files while the server is running. It's not particularly friendly for taking manual backups, but works better when automated. The backup (from the servers perspective) consists of three commands.

<table>
    <thead>
        <tr>
            <th>Command</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>save hold</td>
            <td>This will ask the server to prepare for a backup. It’s asynchronous and will return immediately.</td>
        </tr>
        <tr>
            <td>save query</td>
            <td>After calling `save hold` you should call this command repeatedly to see if the preparation has
                finished. When it returns a success it will return a file list (with lengths for each file) of the files
                you need to copy. The server will not pause while this is happening, so some files can be modified while
                the backup is taking place. As long as you only copy the files in the given file list and truncate the
                copied files to the specified lengths, then the backup should be valid.</td>
        </tr>
        <tr>
            <td>save resume</td>
            <td>When you’re finished with copying the files you should call this to tell the server that it’s okay to
                remove old files again.</td>
        </tr>
    </tbody>
</table>