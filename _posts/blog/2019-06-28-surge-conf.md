---
layout: post
title: Surge.conf规则分享
description: 以DlerCloud+自建节点为例
category: blog
---
# Surge规则分享-以DlerCloud+自建节点为例
---   
## 基础玩法
* `❌token❌`替换成DlerCloud官网上你账户下的`token`

## 进阶玩法
* ` 🇭🇰Dler-IPLC,🇭🇰Dler-BGP,🇯🇵Dler-Relay,🇺🇳Dler-Relay,🇺🇳Dler-Bronze,👤Personal`替换成自己喜欢的名字，并把`policy-path=url`中**url**替换成你机场的surge list订阅链接或通过API转后的list链接
* 注意：`♺PROXY = select,`后的选项也要对应更改，否则会报错

## Surge.conf内容
```

[General]
loglevel = notify
skip-proxy = 192.168.0.0/16, 193.168.0.0/24, 10.0.0.0/8, 172.16.0.0/12, 100.64.0.0/10, 17.0.0.0/8, 127.0.0.1, localhost, *.local
bypass-system = true
internet-test-url = http://www.qualcomm.cn/generate_204
proxy-test-url = http://www.qualcomm.cn/generate_204
test-timeout = 3
dns-server = system, 119.29.29.29, 208.67.222.222, 1.2.4.8, 182.254.116.116,
allow-wifi-access = true
ipv6 = true
external-controller-access = 112233@0.0.0.0:6170
http-listen = 0.0.0.0:5881
socks5-listen = 0.0.0.0:5882
wifi-access-http-port = 5883
wifi-access-socks5-port = 5884
use-default-policy-if-wifi-not-primary = true
shared-jsvm-context = true
show-error-page-for-reject = true
[Proxy]
⭕️DIRECT = direct
🚫Ad-REJ = reject
⛔️Ad-GIF = reject-tinygif

[Proxy Group]
♺PROXY = select, 🇭🇰Dler-IPLC, 🇭🇰Dler-BGP, 🇯🇵Dler-Relay,🇺🇸Dler-Relay,🇺🇳Dler-Relay, 🇺🇳Dler-Global, 👤Personal,ⓌWiFi
♳GlobalTV = select, ♺PROXY, ⭕️DIRECT
♴AsianTV = select, ⭕️DIRECT,♺PROXY,♷Domestic,♳GlobalTV
♵Telegram =select, 🇭🇰Dler-IPLC, 🇭🇰Dler-BGP,🇺🇸Dler-Relay,🇺🇳Dler-Relay,♺PROXY
♶Speedtest = select, ⭕️DIRECT, ♺PROXY
♷Domestic = select, ⭕️DIRECT, ♺PROXY,🇨🇳Dler-Back
♸AdBlock = select, ⛔️Ad-GIF, 🚫Ad-REJ, ⭕️DIRECT
♹Final = select, ⭕️DIRECT,♺PROXY
Apple = select, ⭕️DIRECT, ♺PROXY
ⓌWiFi = ssid, default = 🇭🇰Dler-IPLC, cellular = 🇭🇰Dler-BGP
🇭🇰Dler-IPLC = url-test, policy-path=https://dler.cloud/subscribe/❌token❌?protocols=ss&list=surge&isp=iplc&area=hk, update-interval=0, url=http://www.qualcomm.cn/generate_204, interval=600, tolerance=50
🇭🇰Dler-BGP = url-test, policy-path=https://dler.cloud/subscribe/❌token❌?protocols=ss&list=surge&isp=bgp&area=hk, update-interval=0, url=http://www.qualcomm.cn/generate_204, interval=600, tolerance=50
🇯🇵Dler-Relay = url-test, policy-path=https://dler.cloud/subscribe/❌token❌?protocols=ss&list=surge&type=relay&area=jp, update-interval=0, url=http://www.qualcomm.cn/generate_204, interval=600, tolerance=50
# 🇨🇳Dler-Relay = url-test, policy-path=https://dler.cloud/subscribe/❌token❌?protocols=ss&list=surge&type=relay&area=tw, update-interval=0, url=http://www.qualcomm.cn/generate_204, interval=600, tolerance=50
# 🇸🇬Dler-Relay = url-test, policy-path=https://dler.cloud/subscribe/❌token❌?protocols=ss&list=surge&type=relay&area=sg, update-interval=0, url=http://www.qualcomm.cn/generate_204, interval=600, tolerance=50
🇺🇸Dler-Relay = url-test, policy-path=https://dler.cloud/subscribe/❌token❌?protocols=ss&list=surge&type=relay&area=us, update-interval=0, url=http://www.qualcomm.cn/generate_204, interval=600, tolerance=50
🇺🇳Dler-Relay = select, policy-path=https://dler.cloud/subscribe/❌token❌?protocols=ss&list=surge&type=relay&noarea=hk+jp+us&noisp=back, update-interval=0
🇺🇳Dler-Global = select, policy-path=https://dler.cloud/subscribe/❌token❌?protocols=ss&list=surge&lv=1, update-interval=0
🇨🇳Dler-Back = select, policy-path=https://dler.cloud/subscribe/❌token❌?protocols=ss&list=surge&isp=back, update-interval=0
# 🏳️‍🌈Fly-Vmess = select, policy-path=https://dove.589669.xyz/all2surge?sub=❌url❌&filter=.*NF&emoji=2, update-interval=0
# 👤Personal = select, policy-path=https://gist.githubusercontent.com/Darren-X1/❌token❌/raw/Personal, update-interval=0, url=http://www.qualcomm.cn/generate_204, interval=600, tolerance=50

[Rule]
# Rulesets
RULE-SET,https://raw.githubusercontent.com/lhie1/Rules/master/Surge/Surge%203/Provider/Reject.list,♸AdBlock
RULE-SET,https://raw.githubusercontent.com/lhie1/Rules/master/Surge/Surge%203/Provider/AsianTV.list,♴AsianTV
RULE-SET,https://raw.githubusercontent.com/lhie1/Rules/master/Surge/Surge%203/Provider/GlobalTV.list,♳GlobalTV
RULE-SET,https://raw.githubusercontent.com/lhie1/Rules/master/Surge/Surge%203/Provider/Telegram.list,♵Telegram
RULE-SET,https://raw.githubusercontent.com/lhie1/Rules/master/Surge/Surge%203/Provider/Speedtest.list,♶Speedtest
RULE-SET,https://raw.githubusercontent.com/lhie1/Rules/master/Surge/Surge%203/Provider/Netease%20Music.list,♷Domestic
RULE-SET,https://raw.githubusercontent.com/lhie1/Rules/master/Surge/Surge%203/Provider/Proxy.list,♺PROXY
RULE-SET,https://raw.githubusercontent.com/lhie1/Rules/master/Surge/Surge%203/Provider/Domestic.list,♷Domestic

RULE-SET,SYSTEM,Apple
RULE-SET,https://raw.githubusercontent.com/lhie1/Rules/master/Surge/Surge%203/Provider/Apple.list,Apple

RULE-SET,LAN,DIRECT
DOMAIN,dler.cloud,DIRECT

# > Private Tracker
DOMAIN-SUFFIX,awesome-hd.me,DIRECT
DOMAIN-SUFFIX,broadcasthe.net,DIRECT
DOMAIN-SUFFIX,chdbits.co,DIRECT
DOMAIN-SUFFIX,classix-unlimited.co.uk,DIRECT
DOMAIN-SUFFIX,empornium.me,DIRECT
DOMAIN-SUFFIX,gazellegames.net,DIRECT
DOMAIN-SUFFIX,hdchina.org,DIRECT
DOMAIN-SUFFIX,hdsky.me,DIRECT
DOMAIN-SUFFIX,icetorrent.org,DIRECT
DOMAIN-SUFFIX,jpopsuki.eu,DIRECT
DOMAIN-SUFFIX,keepfrds.com,DIRECT
DOMAIN-SUFFIX,madsrevolution.net,DIRECT
DOMAIN-SUFFIX,m-team.cc,DIRECT
DOMAIN-SUFFIX,nanyangpt.com,DIRECT
DOMAIN-SUFFIX,ncore.cc,DIRECT
DOMAIN-SUFFIX,open.cd,DIRECT
DOMAIN-SUFFIX,ourbits.club,DIRECT
DOMAIN-SUFFIX,passthepopcorn.me,DIRECT
DOMAIN-SUFFIX,privatehd.to,DIRECT
DOMAIN-SUFFIX,redacted.ch,DIRECT
DOMAIN-SUFFIX,springsunday.net,DIRECT
DOMAIN-SUFFIX,tjupt.org,DIRECT
DOMAIN-SUFFIX,totheglory.im,DIRECT

DOMAIN-KEYWORD,announce,DIRECT
DOMAIN-KEYWORD,torrent,DIRECT
DOMAIN-KEYWORD,tracker,DIRECT
DOMAIN-SUFFIX,smtp,DIRECT
URL-REGEX,(Subject|HELO|SMTP),DIRECT
URL-REGEX,(api|ps|sv|offnavi|newvector|ulog.imap|newloc)(.map|).(baidu|n.shifen).com,DIRECT
URL-REGEX,(.+.|^)(360|so|qihoo|360safe|qhimg|360totalsecurity|yunpan).(cn|com),DIRECT
URL-REGEX,(.+.)?(torrent|announce.php?passkey=|tracker|BitTorrent|bt_key|ed2k|find_node|get_peers|info_hash|magnet:|peer_id=|sandai|Thunder|XLLiveUD|xunlei)(..+)?,DIRECT

IP-CIDR,1.1.1.1/24,DIRECT,no-resolve
GEOIP,CN,♷Domestic
FINAL,♹Final,dns-failed

# [Snell Server]
# interface = 0.0.0.0
# port = 5886
# psk = bwh123456
# obfs = off

[SSID Setting]
"X-iPhone" cellular-mode=true

[URL Rewrite]
# GeoIP
^(http|https)://geolite.maxmind.com/download/geoip/database/GeoLite2-Country.tar.gz https://download.maxmind.com/app/geoip_download?edition_id=GeoLite2-Country&license_key=lSf1RH2wWW4MVv6x&suffix=tar.gz 302

# TikTok (By Choler & Paris ^_^)
(?<=(carrier|account|sys)_region=)CN HK 307
(?<=(carrier|account|sys|sim)_region=)cn HK 307

# > Google_Service_HTTPS_Jump
^https?://(www.)?g.cn https://www.google.com 302
^https?://(www.)?google.cn https://www.google.com 302

# > Anti_ISP_JD_Hijack
^https?://coupon.m.jd.com/ https://coupon.m.jd.com/ 302
^https?://h5.m.jd.com/ https://h5.m.jd.com/ 302
^https?://item.m.jd.com/ https://item.m.jd.com/ 302
^https?://m.jd.com/ https://m.jd.com/ 302
^https?://newcz.m.jd.com/ https://newcz.m.jd.com/ 302
^https?://p.m.jd.com/ https://p.m.jd.com/ 302
^https?://so.m.jd.com/ https://so.m.jd.com/ 302
^https?://union.click.jd.com/jda? http://union.click.jd.com/jda?adblock= header
^https?://union.click.jd.com/sem.php? http://union.click.jd.com/sem.php?adblock= header
^https?://www.jd.com/ https://www.jd.com/ 302

# > Anti_ISP_Taobao_Hijack
^https?://m.taobao.com/ https://m.taobao.com/ 302

# > Wiki
^https?://.+.(m.)?wikipedia.org/wiki http://www.wikiwand.com/en 302
^https?://zh.(m.)?wikipedia.org/(zh-hans|zh-sg|zh-cn|zh(?=/)) http://www.wikiwand.com/zh 302
^https?://zh.(m.)?wikipedia.org/zh-[a-zA-Z]{2,} http://www.wikiwand.com/zh-hant 302

# > NOMO
^https://nomo.dafork.com/api/v3/iap/ios_product_list https://files.catbox.moe/fgmkpy.json 302

# > Other
^https?://cfg.m.ttkvod.com/mobile/ttk_mobile_1.8.txt http://ogtre5vp0.bkt.clouddn.com/Static/TXT/ttk_mobile_1.8.txt header
^https?://cnzz.com/ http://ogtre5vp0.bkt.clouddn.com/background.png? header
^https?://m.qu.la/stylewap/js/wap.js http://ogtre5vp0.bkt.clouddn.com/qu_la_wap.js 302
^https?://m.yhd.com/1/\? http://m.yhd.com/1/?adbock= 302
^https?://n.mark.letv.com/m3u8api/ http://burpsuite.applinzi.com/Interface header
^https?://sqimg.qq.com/ http://sqimg.qq.com/ 302
^https?://static.m.ttkvod.com/static_cahce/index/index.txt http://ogtre5vp0.bkt.clouddn.com/Static/TXT/index.txt header
^https?://www.iqshw.com/d/js/m http://burpsuite.applinzi.com/Interface header
^https?://www.iqshw.com/d/js/m http://rewrite.websocket.site:10/Other/Static/JS/Package.js? header

[MITM]
skip-server-cert-verify = true
tcp-connection = false

hostname= *.jd.com,*taobao.com,*.maxmind.com, api*.tiktokv.com, api*.amemv.com, *.tiktokcdn.com, api*.musical.ly,*.360buyimg.com,*.chelaile.net.cn,*.cnbetacdn.com,*.didistatic.com,*.doubanio.com,*.google-analytics.com,*.iydsj.com,*.k.sohu.com,*.kfc.com,*.kingsoft-office-service.com,*.meituan.net,*.ofo.com,*.pixiv.net,*.pstatp.com,*.uve.weibo.com,*.wikipedia.org,*.wikiwand.com,*.ydstatic.com,*.youdao.com,*.youtube.com,*.zhuishushenqi.com,*.zymk.cn,101.201.62.22,113.105.222.132,113.96.109.*,118.178.214.118,119.18.193.135,121.14.89.216,121.9.212.178,123.59.31.1,14.21.76.30,153.3.236.81,180.101.212.22,183.232.237.194,183.232.246.225,183.60.159.227,218.11.3.70,59.151.53.6,59.37.96.220,789.kakamobi.cn,a.apicloud.com,a.applovin.com,a.qiumibao.com,a.sfansclub.com,a.wkanx.com,aarkissltrial.secure2.footprint.net,acs.m.taobao.com,act.vip.iqiyi.com,activity2.api.ofo.com,adm.10jqka.com.cn,adproxy.autohome.com.cn,adse.ximalaya.com,afd.baidu.com,api*.musical.ly,api*.tiktokv.com,api.abema.io,api.app.vhall.com,api.bilibili.com,api.chelaile.net.cn,api.daydaycook.com.cn,api.douban.com,api.feng.com,api.fengshows.com,api.gotokeep.com,api.huomao.com,api.intsig.net,api.jr.mi.com,api.jxedt.com,api.k.sohu.com,api.kkmh.com,api.laifeng.com,api.live.bilibili.com,api.m.mi.com,api.mddcloud.com.cn,api.mgzf.com,api.psy-1.com,api.rr.tv,api.smzdm.com,api.tv.sohu.com,api.wallstreetcn.com,api.weibo.cn,api.xiachufang.com,api.zhihu.com,api.zhuishushenqi.com,api5.futunn.com,api-mifit.huami.com,api-mifit-cn.huami.com,api-release.wuta-cam.com,app.10086.cn,app.58.com,app.api.ke.com,app.bilibili.com,app.m.zj.chinamobile.com,app.mixcapp.com,app.variflight.com,app.wy.guahao.com,app2.autoimg.cn,appsdk.soku.com,atrace.chelaile.net.cn,b.zhuishushenqi.com,c.m.163.com,cap.caocaokeji.cn,capi.douyucdn.cn,capi.mwee.cn,cdn.kuaidi100.com,cdn.moji.com,channel.beitaichufang.com,classbox2.kechenggezi.com,client.mail.163.com,cms.daydaycook.com.cn,connect.facebook.net,consumer.fcbox.com,creatives.ftimg.net,creditcard.ecitic.com,d.1qianbao.com,daoyu.sdo.com,dapis.mting.info,dl.app.gtja.com,dongfeng.alicdn.com,dsp-impr2.youdao.com,dspsdk.abreader.com,e.dangdang.com,erebor.douban.com,fdfs.xmcdn.com,fm.fenqile.com,frodo.douban.com,fuss10.elemecdn.com,g1.163.com,gateway.shouqiev.com,gorgon.youdao.com,gw.alicdn.com,gw-passenger.01zhuanche.com,hm.xiaomi.com,hui.sohu.com,huichuan.sm.cn,i.weread.qq.com,i.ys7.com,i1.hoopchina.com.cn,iapi.bishijie.com,iface.iqiyi.com,iface2.iqiyi.com,img*.doubanio.com,img.jiemian.com,img.zuoyebang.cc,img01.10101111cdn.com,img1.126.net,img1.doubanio.com,img3.doubanio.com,impservice.dictapp.youdao.com,impservice.youdao.com,interface.music.163.com,ios.prod.ftl.netflix.com,ios.wps.cn,kano.guahao.cn,lives.l.qq.com,m*.amap.com,m.aty.sohu.com,m.client.10010.com,m.creditcard.ecitic.com,m.ibuscloud.com,m.yap.yahoo.com,m5.amap.com,ma.ofo.com,mage.if.qidian.com,mapi.appvipshop.com,mapi.mafengwo.cn,mapi.weibo.com,mbl.56.com,media.qyer.com,mi.gdt.qq.com,mimg.127.net,mmg.aty.sohu.com,mmgr.gtimg.com,mob.mddcloud.com.cn,mobile-api2011.elong.com,mp.weixin.qq.com,mrobot.pcauto.com.cn,mrobot.pconline.com.cn,ms.jr.jd.com,msspjh.emarbox.com,newsso.map.qq.com,nex.163.com,nnapp.cloudbae.cn,open.qyer.com,p.kuaidi100.com,p1.music.126.net,pic.k.sohu.com,pic1.chelaile.net.cn,pic1cdn.cmbchina.com,pic2.zhimg.com,portal-xunyou.qingcdn.com,pss.txffp.com,r.inews.qq.com,render.alipay.com,resource.cmbchina.com,res-release.wuta-cam.com,ress.dxpmedia.com,richmanapi.jxedt.com,rm.aarki.net,rtbapi.douyucdn.cn,service.4gtv.tv,slapi.oray.net,smkmp.96225.com,snailsleep.net,sp.kaola.com,ssl.kohsocialapp.qq.com,sso.ifanr.com,static.api.m.panda.tv,static.vuevideo.net,static1.keepcdn.com,staticlive.douyucdn.cn,storage.wax.weibo.com,support.you.163.com,supportda.ofo.com,thor.weidian.com,ups.youku.com,wapwenku.baidu.com,wenku.baidu.com,www.dandanzan.com,www.facebook.com,www.flyertea.com,www.ft.com,www.oschina.net,www.zhihu.com,youtubei.googleapis.com,zhidao.baidu.com

enable = true

ca-passphrase = UNCLEWANG
ca-p12 = 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

[Script]
# > Weibo
http-response ^https?://m?api\.weibo\.c(n|om)/2/(statuses/(unread|extend|positives/get|(friends|video)(/|_)timeline)|stories/(video_stream|home_list)|(groups|fangle)/timeline|profile/statuses|comments/build_comments|photo/recommend_list|service/picfeed|searchall|cardlist|page|\!/photos/pic_recommend_status) requires-body=1,script-path=https://raw.githubusercontent.com/yichahucha/surge/master/wb_ad.js
http-response ^https?://(sdk|wb)app\.uve\.weibo\.com(/interface/sdk/sdkad.php|/wbapplua/wbpullad.lua) requires-body=1,script-path=https://raw.githubusercontent.com/yichahucha/surge/master/wb_launch.js

# > WeChat
http-request ^https://mp\.weixin\.qq\.com/mp/getappmsgad script-path=https://Choler.github.io/Surge/Script/WeChat.js

# > Youtube
http-request ^https://[\s\S]*\.googlevideo\.com/.*&(oad|ctier) script-path=https://Choler.github.io/Surge/Script/YouTube.js

# > Aweme
http-response ^https://[\s\S]*\/aweme/v1/(feed|aweme/post|follow/feed)/ requires-body=1,max-size=-1,script-path=https://Choler.github.io/Surge/Script/Aweme.js
http-response ^https?://[a-z]*\.snssdk\.com/bds/feed/stream/ requires-body=1,max-size=-1,script-path=https://Choler.github.io/Surge/Script/Super.js

# > Toutiao
http-response ^https?://[\s\S]*\.snssdk\.com/api/news/feed/v88/ requires-body=1,max-size=-1,script-path=https://Choler.github.io/Surge/Script/Toutiao.js

# > Kaola
http-request ^https://sp\.kaola\.com/api/openad$ script-path=https://Choler.github.io/Surge/Script/Kaola.js

# > QQ News
http-response https://r\.inews\.qq.com\/get(QQNewsUnreadList|RecommendList) requires-body=1,max-size=-1,script-path=https://Choler.github.io/Surge/Script/QQNews.js

# > RRad
http-response ^https://api\.rr\.tv/v3plus/index/(channel|todayChoice)$ requires-body=1,max-size=-1,script-path=https://Choler.github.io/Surge/Script/RRad.js

# > Zhihu
http-response ^https://api.zhihu.com/moments\?(action|feed_type) requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/Surge-Script/master/surge%20zhihu%20feed.js
http-response ^https://api.zhihu.com/topstory/recommend requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/Surge-Script/master/surge%20zhihu%20recommend.js
http-response ^https://api.zhihu.com/v4/questions requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/Surge-Script/master/surge%20zhihu%20answer.js
http-response ^https://api.zhihu.com/people/ requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/Surge-Script/master/surge%20zhihu%20people.js

# > Bilibili
http-response ^https://app.bilibili.com/x/v2/space\?access_key requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/Surge-Script/master/surge%20bilibili%20space.js
http-response ^https://app.bilibili.com/x/resource/show/tab\?access_key requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/Surge-Script/master/surge%20bilibili%20tab.js
http-response ^https://app.bilibili.com/x/v2/feed/index\?access_key requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/Surge-Script/master/surge%20bilibili%20feed.js
http-response ^https://app.bilibili.com/x/v2/account/mine\?access_key requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/Surge-Script/master/surge%20bilibili%20account.js
http-response ^https://app.bilibili.com/x/v2/view\?access_key requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/Surge-Script/master/surge%20bilibili%20view%20relate.js
http-response ^https://api.live.bilibili.com/xlive/app-room/v1/index/getInfoByRoom\?access_key requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/Surge-Script/master/surge%20bilibili%20live.js
http-response ^https://api.bilibili.com/pgc/view/app/season requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/UnblockBangumi/master/surge/surge%20bilibili%20season.js
http-response ^https://api.bilibili.com/pgc/player/api/playurl requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/onewayticket255/UnblockBangumi/master/surge/surge%20bilibili%20playurl.js



# > Display Netflix TV series and movie's IMDb ratings, Douban ratings, rotten tomato and country/region
http-request ^https?://ios\.prod\.ftl\.netflix\.com/iosui/user/.+path=%5B%22videos%22%2C%\d+%22%2C%22summary%22%5D script-path=https://raw.githubusercontent.com/yichahucha/surge/master/nf_rating.js
http-response ^https?://ios\.prod\.ftl\.netflix\.com/iosui/user/.+path=%5B%22videos%22%2C%\d+%22%2C%22summary%22%5D requires-body=1,script-path=https://raw.githubusercontent.com/yichahucha/surge/master/nf_rating.js

# > Display commodity historical price - JD
// http-response ^https?://api\.m\.jd\.com/client\.action\?functionId=(wareBusiness|serverConfig) requires-body=1,script-path=https://raw.githubusercontent.com/yichahucha/surge/master/jd_price.js

# > Display commodity historical price - Taobao
// http-response ^https://trade-acs.m.taobao.com/gw/mtop.taobao.detail.getdetail requires-body=1,script-path=https://raw.githubusercontent.com/yichahucha/surge/master/tb_price.js


```

---

[![1](https://tva1.sinaimg.cn/large/0082zybpgy1gbslxkn7txj31sc07qwg2.jpg)](https://t.me/net_door)
