> [bds_doc_cn](http://github.com/ShrBox/bds_doc_cn) by [ShrBox](http://github.com/ShrBox)

# **如何使用基岩版专用服务器**

## **免责声明**

这是我们尚未完全支持的早期alpha版本，它可能存在严重的问题，我们会随时停止支持。

## **推荐配置**

我们推荐在至少拥有两个核心和1Gb内存的64位Intel或AMD处理器的服务器上运行基岩版专用服务器。

## **平台**

### **Linux**

Linux版本的基岩版专用服务器需要Ubuntu 18及以上的版本，不支持除Ubuntu外其它的发行版</br>
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
            <th>何时使用</th>
            <th>备注</th>
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
            <td>任何字符串(String)</td>
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
            <td>任何字符串(String)</td>
            <td>level</td>
            <td>始终</td>
            <td>被使用/创建的世界的名字。每个世界都在`/worlds`中有自己的文件夹</td>
        </tr>
        <tr>
            <td>level-seed</td>
            <td>任何字符串(String)</td>
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
                无论此设置项如何，连接到远程(非局域网)服务器的客户端始终需要登录微软账户。
                如果服务器接受来自互联网的连接(开放给所有玩家游玩)，我们<b>非常</b>推荐打开online-mode</td>
        </tr>
        <tr>
            <td>white-list</td>
            <td>true, false</td>
            <td>false</td>
            <td>始终</td>
            <td>如果值为true则所有连接的玩家必须存在于<code>whitelist.json</code>文件中
                请参考<a href="#白名单">白名单</a>部分</td>
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
            <td>在异常移动次数增加之前，服务器和客户端位置可能不同步的持续时间(由<code>player-movement-distance-threshold</code>定义)。以毫秒为单位
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

当解压时你会看到一些文件夹和可执行文件。</br>
当服务器启动时将会创建一堆空文件夹。</br>
您应该关注如下文件夹:

<table>
    <thead>
        <tr>
            <th>文件夹名</th>
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
            <td>如果这个文件夹不存在，则会在服务器启动时创建。世界会在一个特定文件夹中创建，文件夹名根据<code>server.properties</code>中的<code>level-name</code>配置项而定</td>
        </tr>
    </tbody>
</table>

## **白名单**

如果在 `server.properties` 中的 `white-list` 项为true，那么服务器将只允许已被添加进白名单的玩家连接。如果您要允许玩家连接，你就需要知道他们的玩家ID。将一个玩家添加到白名单中最简易的方法就是使用命令`whitelist add "Gamertag"` (例如: `whitelist add ExampleName`)。注意：如果玩家ID中包含空格，你需要用双引号来将玩家ID引起来：`whitelist add "Example Name"`

之后如果你想要将某人从白名单中移除，可以使用命令：`whitelist remove "Gamertag"`

白名单将会被保存在 `whitelist.json`文件中。如果您想要自动化处理白名单玩家的增加与删除，您可以这么做。在您修改了文件之后您需要执行命令：`whitelist reload` 来确保服务器加载了变更

该文件包含了一个JSON数组，其对象包含以下键/值。

<table>
    <thead>
        <tr>
            <th>键</th>
            <th>类型</th>
            <th>值</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>name</td>
            <td>String(字符串)</td>
            <td>玩家的ID</td>
        </tr>
        <tr>
            <td>xuid</td>
            <td>String(字符串)</td>
            <td>(可选)玩家的xuid。如果此项为空则此项将会在玩家进入服务器时自动填充</td>
        </tr>
        <tr>
            <td>ignoresPlayerLimit</td>
            <td>Boolean(true/false)</td>
            <td>如果为true则该玩家不会被计入最大玩家限制。目前，
                即使有玩家使用此选项，也存在30(或比指定的最大玩家数高1)个已连接玩家的软限制。</br>
                这样做的目的是即使服务器已满，也让一些玩家能够加入。</td>
        </tr>
    </tbody>
</table>

示例 `whitelist.json` 文件:

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

你可以通过在被放置在服务器可执行文件同一文件夹的 `permissions.json` 文件来分配玩家的角色，以调整玩家的特定的权限。该文件包含具有XUID和权限的简单JSON对象。 有效的权限有:`operator`(OP), `member`(成员), `visitor`(访客)。与这些帐户相关联的每个玩家都将根据设置的权限进行处理。如果你在服务器运行时修改了这个文件，则需要执行命令：`permissions reload` 来确保服务器加载了修改。你也可以运行 `permissions list` 命令来列出当前已分配的权限。请注意，由于xuid需要在线验证用户的帐户，因此需要启用`online-mode`才能使此功能起作用。如果一个没有在此列表中的玩家连接，`server.properties`中的`default-player-permission-level`选项将会起作用

示例 `permissions.json` 文件:

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
        "xuid": "1145141919"
    }
]<
```

## **崩溃报告**

如果服务器崩溃，它将自动向我们发送各种信息，以帮助我们在未来解决问题。

## **命令**

你可以通过在控制台中输入来在服务器中执行命令。以下命令是可用的。其中，< >意味着一个参数是必须的，[ ]意味着这是可选的并且|表示不同的允许值。如果字符串包含空格可以用双引号引起来。

<table>
    <thead>
        <tr>
            <th>命令语法</th>
            <th>说明</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>kick <玩家名或xuid> [原因]</td>
            <td>立刻<del>让一个玩家gck</del>踢出一个玩家。
            </br>原因将被展示在被踢出玩家的屏幕上</td>
        </tr>
        <tr>
            <td>stop</td>
            <td>优雅地停止服务器</td>
        </tr>
        <tr>
            <td>save &lt;hold | resume | query&gt;</td>
            <td>用于在服务器运行时进行热备份。有关更多信息，请参见<a href="#备份">备份</a>部分。
            </td>
        </tr>
        <tr>
            <td>whitelist &lt;on | off | list | reload&gt;</td>
            <td>
                <code>on</code>和<code>off</code>用于打开和关闭白名单。注意这不会改变在<code>server.properties</code>文件中的值！</br></br>
                <code>list</code> 打印服务器当前使用的白名单列表</br></br>
                <code>reload</code> 让服务器从文件中重载白名单</br></br>
                更多信息请参见<a href="#白名单">白名单</a>部分
            </td>
        </tr>
        <tr>
            <td>whitelist &lt;add | remove&gt; &lt;name&gt;</td>
            <td>从白名单文件中添加或删除玩家。
                name参数必须是你想移除的玩家的ID或xuid。
                您无需在这里指明xuid，玩家首次连接时xuid就会被与id绑定。</br></br>
                更多信息请参见<a href="#白名单">白名单</a>部分</td>
        </tr>
        <tr>
            <td>permission &lt;list | reload&gt;</td>
            <td>
                <code>list</code> 打印当前的权限列表</br></br>
                <code>reload</code> 让服务器从文件中重载权限列表</br></br>
                更多信息请参见<a href="#权限">权限</a>部分
            </td>
        </tr>
        <tr>
            <td>op &lt;player&gt;</td>
            <td>
                提升一个玩家的等级到<code>operator</code>(OP)。如果玩家通过了微软账户验证，那么操作将被写入到 <code>permissions.json</code> 中。如果 <code>permissions.json</code> 不存在将会被自动创建。如果玩家没有通过微软账户验证，那么该操作将不会被写入到硬盘而是仅被写入到内存中</br>
                服务器重新启动后默认的权限等级将会被分配给玩家
            </td>
        </tr>
        <tr>
            <td>deop &lt;player&gt;</td>
            <td>
                将一个玩家降级为<code>member</code>(成员)。如果玩家通过了微软账户验证，那么操作将被写入到 <code>permissions.json</code> 中。</br>
                如果 <code>permissions.json</code> 不存在将会被自动创建。
            </td>
        </tr>
        <tr>
            <td>changesetting &lt;setting&gt; &lt;value&gt;</td>
            <td>在不重启服务器的情况下修改设置。当前只有两个设置项支持被修改，<code>allow-cheats</code>(允许作弊命令，true或false)和 <code>difficulty</code>(难度，<code>peaceful</code>(和平), <code>easy</code>(简单), <code>normal</code>(普通), 或 <code>hard</code>(困难))。</br>
            使用该命令不会修改<code>server.properties</code>中的配置项</td>
        </tr>
    </tbody>
</table>

## **备份**

基岩版专用服务器支持在服务器运行时备份世界文件。这对手工备份极其不友好，但是当您使用自动化时会工作得更好。备份(从服务器角度来看)由三个命令组成。

<table>
    <thead>
        <tr>
            <th>命令</th>
            <th>说明</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>save hold</td>
            <td>这将会告诉服务器为备份做准备。它是异步的并且将立刻返回结果</td>
        </tr>
        <tr>
            <td>save query</td>
            <td>在执行<code>save hold</code>后你应该反复执行此命令来查看准备工作是否完成。
            当它返回成功时它将会输出你需要拷贝的文件的列表(附带每一个文件的长度)。当这事进行时服务器不会暂停，
            所以一些文件可以在备份的过程中被修改。您只需要拷贝给出的文件列表并将复制的文件截断为指定的长度，备份应该会是有效的</td>
        </tr>
        <tr>
            <td>save resume</td>
            <td>当您已经完成了文件拷贝您应该使用这条命令来告诉服务器<del>我好了</del>可以删除旧的文件了</td>
        </tr>
    </tbody>
</table>