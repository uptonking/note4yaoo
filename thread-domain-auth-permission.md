---
title: thread-domain-auth-permission
tags: [auth, community, permission, solutions]
created: 2025-09-22T13:53:24.806Z
modified: 2025-09-22T13:53:51.831Z
---

# thread-domain-auth-permission

# guide

- features
  - authentication
  - authorization: rbac
  - docker deploy
  - multi-tenancy
  - scaling

- tips
  - 选择成熟方案的优点: 方便搜索已知问题, ai对已有资源更熟练
# discuss-stars
- ## 

- ## 

- ## 

- ## [A/B tested password vs magic link vs passkey signup. Embarassing conversion difference. : r/reactjs _202604](https://www.reddit.com/r/reactjs/comments/1swygdc/ab_tested_password_vs_magic_link_vs_passkey/)
  - Timeline - 2 weeks. Got roughly 3000 signups per variant.
  - Password-first: 61% completion, 3m 42s to dashboard
  - Magic link: 79% completion, 1m 15s to dashboard
  - Passkey-first (magic link fallback): 74% completion, 48 seconds to dashboard
  - We eventually opted for passkey-first, felt like an obvious choice despite lower initial conversion compared to magic link.
  - Retention was also higher as passkey users come back more because returning login is just a biometric tap.
  - Some context: the reason we tested all 3 is because descope's flow builder let us design each variant visually and switch between them without code changes.

- What kind of platforms are your users on? Seems passkey works better on Macs

- ## [Should we do authentication in house or outsource? : r/webdev _202402](https://www.reddit.com/r/webdev/comments/1akm37q/should_we_do_authentication_in_house_or_outsource/)
- having built several of them myself and often used djangos pre made auth, i would still go with Keycloak if you plan to have either multi client or distributed backend. 
  - Authentication isnt my main business, why should i spend time build something that already exists that I can get for free, even if its "not hard". 
  - The saved time can be used to improve keycloak if you really want to build auth services.

- NextAuth.js, now Auth.js, is the library you run on top of your frontend app to connect to any of these oauth services. 
  - Auth.js just makes it easier to use an oauth provider, it doesnt actually authenticate users.

- You need to factor in long term maintenance, including software upgrades as security changes and keeping a close watch on that server. Just because something is possible doesn’t make it the right decision 
- Keycloak is a good choice at the start, but there are extra things to take into account like maintenance and upgrade of the Keycloak, this might be cumbersome if you have a small team so I'd suggest going with an external provider like Okta.

- Coding an auth system isn't hard at all, unless you need a super safe system and/or work with high risk content. I try to avoid 3rd party services as much as I can. Vendor lock in, fees, etc

- Don’t handle your own auth. There are smarter, better devs who have built much more secure systems than you could hack together.

- I would use the outsourced provider because you can have a faster Time to Market, cheaper at small scale (don't need to invest in learning these technologies in depth), more features, easy onboarding of new users via social logins (google, github, facebook etc.).

- That's why I choose Laravel for 90% of my projects. It takes care of that out of the box and 100 other things at the same time.

- ## [Why use Authentik/Authelia over built in authentication? : r/homelab _202508](https://www.reddit.com/r/homelab/comments/1mfn2k5/why_use_authentikauthelia_over_built_in/)
- Built-in auth means 10 ways to log in. Authentik/Authelia give you one master key—central control, no duplicate logins. Why juggle when you can simplify?

- The benefit of it is it is SSO, single sign on.
- So instead of havin a separate user account for each service, I would just have the account in Authentik and can log into every service which supports SSO?
  - Sort of. You still have an account with each service.
  - Just instead of needing to use a username and password you can just log in with SSO.
  - Like reddit supports login with Google. You still have a reddit account, but you don't have a password, you just login via Google.

- Why: Central user management. Ability to add MFA to services that may not natively support it. Ability to login once and automatically be authenticated across services.
  - And yeah, it either would replace outright, or provide another option to, login to a service.

- In my use case, I have a single login page that protects all my services. Traefik is my reverse proxy and handles all the certificates automatically (setting up and renewing) and Authelia is my middleware.

- A single credential, and centralized RBAC
# discuss-tips/pattern
- ## 

- ## 

- ## 

- ## 
# discuss-auth-client/ui
- ## 

- ## 

- ## 

- ## 

- ## [What Auth provider? : r/nextjs _202506](https://www.reddit.com/r/nextjs/comments/1li4mx7/what_auth_provider/)
- Personally for my use case Better Auth makes more sense. It’s more customizable than Clerk.
  - Yeah, I have worked with Clerk, and the overall customizablity is so bad. The UI, the logic, you will feel writing the auth(backend part) from scratch. I think Kinde and 0Auth is better. If you're using Firebase or Supabase, using their own auth.

- I previously used Clerk due to how simple it was to set up, but the UI and UX was so terrible. It felt like an alien in my application due to the lack of in-depth customization.
  - Better auth seems like the best option at the moment. They permit so many features using their plugin system and i love it. They even have some features that you have to pay for using Clerk.

- Clerk auth just added subscriptions through stripe and I must say, it’s a game changer. Easy to lock down pages and have lots of features and payment tiers.

- Authentication provider shouldn't matter much since in properly designed system it can be swapped anytime. 

- I started using supabase a while ago. While great at first, you're being quickly locked down to their infra.
  - For example if client has a specific need or the project really doesn't need postgres and a simple sqllite would work well, you cannot easily migrate from it.
- Firebase Auth is so great and very generous, but the firestore database is a mess in my opinion. Supabase is a way better option at this point

- ## [Does anyone not like better-auth? : r/nextjs _202507](https://www.reddit.com/r/nextjs/comments/1m3tcg3/does_anyone_not_like_betterauth/)
- I’m the actual maintainer :) We’ll have a lot more people involved soon now that we have some funding to push things forward.

- I wish I could use it without the DB.

- ## [Any drawbacks to using Better-Auth in production? : r/nextjs](https://www.reddit.com/r/nextjs/comments/1mmbfm4/any_drawbacks_to_using_betterauth_in_production/)

- You can't use it if your backend isn't JavaScript. That's about it.

- It’s quite opinionated - even though it’s got a plugin system, multi tenancy was still a bitch to figure out (different users with the same email address)

- ## [Is Better Auth really any better : r/nextjs _202508](https://www.reddit.com/r/nextjs/comments/1mk9219/is_better_auth_really_any_better/)
- Speaking from my limited experience. AuthJS was a hot mess. Even basic things like missing documentation and basic examples not working. For something that was supposed to be the standard back in those days, it was mind-boggling. I straight up gave up on nexjs because of autjs/nextauth.
  - Then sometimes after I tried better auth (still was in early stages), and it was miles better IMO, especially for DX. And I believe its only gotten better and more mature since then.
- Agreed, and also, the 2 parallel version mess (5 beta and 4) is freaking terrible. You may find some doc or smippet that doesnt work because of this, which sucks. I've migrated from Authjs to betterAuth and it was smooth.

- Better Auth is one of the few libraries from my experience that just worked amazing out of the box. Documentation is great and has a good ecosystem of plugins. Highly recommend using it.

- BetterAuth, IMO - which is limited in the Typescript space compared to some of these devs - is by far the best I’ve used.

- I haven't *once* been confused by Better-Auth's documentation. AuthJS was a mess, and Lucia was a bit hard to digest.

- BetterAuth I’d say is an easy second. It’s complex in implementation but the boilerplate and docs made it very easy. And it’s BYO-everything so about as cost efficient as it gets for 2FA, passwordless etc. And the complexity comes in handy in unique situations

- ## [Clerk vs BetterAuth : r/nextjs _202508](https://www.reddit.com/r/nextjs/comments/1mzl34w/clerk_vs_betterauth/)
- You can self host better-auth and keep all your data in the same db as your app, no need for calling separate service with separate db, no need for paying monthly fee just to be able to authenticate your users.

- I like self-hosting (sometimes), but I don't like having a user table in my app DB. I prefer auth being a separate service, which is why I like openauth.
  - I prefer not to store user data in my app's database because it simplifies the overall architecture, it's easier to maintain in the long-term, and reduces the risk of having sensitive information mixed with core app data. Also, it makes it easier to reuse the same auth system across multiple apps or services.
  - There is a reason why most big companies use separate auth services and even pay for third party services.
- You can do it with better-auth, too. You can have your own auth service and use the URL to initiate an auth instance in the other services.

- Clerk is solid. The reason people talk about BetterAuth is control. It lives in your own codebase, works closely with Next js, and avoids vendor lock in. Some folks prefer that approach. If you are happy with Clerk and the pricing works for you, you are not missing much.

- ## [Why does everyone recommend Clerk/Auth0/etc when NextAuth is this easy?? : r/nextjs _202504](https://www.reddit.com/r/nextjs/comments/1k02xki/why_does_everyone_recommend_clerkauth0etc_when/)
- Authjs has far fewer features than Clerk, which covers more than just authentication (roles management, organization management, etc). Betterauth has most of these things

- next-auth is currently transitioning to auth.js and it’s not been the smoothest upgrade path. And to be honest, I don’t really like the auth.js implementation.

- Some companies don't want to manage user data. data breaches, GDPR, etc are big risks if you don't do it right. My company doesn't want to manage user data, so we use a third party for user data and authentication instead.
- The difference is mainly managing user sessions and data strictly in a security and cryptographic sense. We use Auth0 at work for all of our apps simply because we don’t need to care about quite a whole lot.

- Because implementing it covers only 1/4 of the whole auth and authorisation and security concerns. 
  - You still need to handle password recovery, user recovery, mfa, securing data at rest. Also it goes without warranty if you use byo auth. Oh also, scaling.

- It definitely is paid promotion by influencers on youtube and X. Right now better auth has the best dev experience to implement on our own - oAuth, anonymous, user-impersonation, organizations, takes a hour to implement complex workflows too.
  - but the only use case I think it's worth for is B2B products in regulated industries like fintech, where compliance is huge factor, and existing enterprise solutions like auth0 are very expensive. but it's definitely a not worth for b2c or free / freemium apps

- ## [Comparing popular auth solutions for Next.js (Lucia, Next Auth v5, Clerk) : r/nextjs _202409](https://www.reddit.com/r/nextjs/comments/1fea4a6/comparing_popular_auth_solutions_for_nextjs_lucia/)
- supabase auth should be here
  - Have been using Supabase for quite a while but I don’t like the way they didn’t handle deduplicate users. Not the worst DX but love to learn new alternatives out there

- Lucia is the best, you presented it in image as bullshit. It is at perfect sweet point of abstraction level. NextAuth is too black boxy and requires like 30 columns in DB. Lucia requires 5.

- I’ve used both Lucia and next-auth/authjs. I feel like the comparison suggested here is, although true, not entirely fair. Lucia is not a complete solution, it is meant to be a utility API

- ## [Comparing Auth from Supabase, Firebase, Auth.js, Ory, Clerk and others : r/selfhosted _202302](https://www.reddit.com/r/selfhosted/comments/114kufp/comparing_auth_from_supabase_firebase_authjs_ory/)
- Keycloak isn't an auth solution (at least in the way of having app integrations or an SDK), it's an identity manager. It's closer to a self hosted Azure active directory than anything else.

# discuss-auth-vendors
- ## 

- ## 

- ## [2FA For Ente Auth Itself? : r/enteio _202502](https://www.reddit.com/r/enteio/comments/1ih3jrj/2fa_for_ente_auth_itself/)
- I don’t think it is standard to have 2FA on your 2FA app. If you did you would then want another 2FA to protect that one, resulting in an endless line of 2FA apps protecting the previous 2FA app. Eventually you would end up with a 2FA app that you just can’t protect with 2FA. Best bet is to use an awesome password for Ente that you don’t use anywhere else and that you physically backup to some offline place like a safety deposit box or something.
- Honestly it is confusing for me: Ente Photos allows you to enable 2FA. I would want 2FA on my Ente Photos because that is just common good practice. But not on my Ente Authenticator! That would be weird. Since it is the same acount. I have Bitwarden.eu as password manager, I could store my Ente account 2FA there but then, it again makes no sense, since to login to Bitwarden I would also need a 2FA code from Ente.. I end up in a loop and also, its not really 2FA anymore then.
- 总有一个帐号不能添加2fa，否则就循环依赖了

- To enable TOTP for Ente itself you have to enable it from the Photos app
  - Just don’t store the 2fa for Ente only in Ente Auth, Make backups, always

- you prob want to take a look at use of passkey  [Introducing Passkeys on Ente _202406](https://ente.com/blog/introducing-passkeys-on-ente/)

- [2fa for ente auth : r/enteio _202604](https://www.reddit.com/r/enteio/comments/1sou2xc/2fa_for_ente_auth/)
  - My ente auth account is not tied to my regular ente account. For that reason I don't use 2FA on the ente auth account but do on my main ente account. All passwords are stored in KeePassXC / KeePassDX.
  - This separate account for auth and photos is even suggested by Ente when setting up Auth to ensure you don't end up in a loop of needing 2FA to login to photos but needing the same 2FA to login to auth. I think they call it enteception.

- ## [Between ENTE, 2FAS, GAuth, Microsoft Auth, DUO and Authy, what are the best authenticator apps? : r/Bitwarden _202509](https://www.reddit.com/r/Bitwarden/comments/1nbdob3/between_ente_2fas_gauth_microsoft_auth_duo_and/)
- Both ente and 2fas allow local backup. 
- A nice feature of Ente is that it shows you both the current and the next code, so you never have to hurry.
  - 2FAS also shows both codes when the time is less than 10 sec

- Aegis
  - No iOS version unfortunately. 

- Google Authenticator, MS Authenticator, Duo, and Authy all use super duper sneaky secret source code. There is no way of knowing if thieves or a hostile government agency has compromised the app.
  - Bitwarden Authenticator is very new, and it shows a lot of promise.
  - Bitwarden Authenticator is very new, and it shows a lot of promise.
  - Ente Auth covers all the bases. It has a zero knowledge cloud backing store. It allows you to export the datastore, so you are not relying on the vendor to not crash and lose your data.
  - Ente also runs on Windows, Mac, Linux, Android, and iOS. The datastore is interoperable, unlike 2FAS where your backing store is EITHER Google or Apple, and there is no connection.

- All apps from which you can store a local backup AND easily export your OTP-keys, if you ever need to change authenticator. Period.
  - Microsoft, Google and the vast majority of the big tech apps, do not allow you to export your data. That is, you’ll be locked in and it’s a real hassle to renew all individual codes if you ever must change authenticator in the future. I’ve been there, I’ve done that.
  - As for me, I settled with Ente. I was very close to go with 2FAS, but they fell short on no native desktop support, only relying on browser extensions (if I remember correctly). Proton has recently also released a 2FA app with the same properties (local copy and export), and would indeed have been another competitor back then.
  - However, remember not to use an authenticator from the same provider you use for password management (with sync!). It’s the most common mistake people do. It defeats the purpose of 2FA. If bad people ever get hold of your master password for your passwords and secrets, they will also have access to your 2FA codes. Hence, it’s 2FA without being 2FA.

- I would avoid the non open source ones: Google, Microsoft, DUO, and Authy are no go. It needs to be both open source and E2EE for syncing, or local syncing to me. That said, I personally use Ente Auth, but many people seem to enjoy 2FAS as well.

- why not using the Bitwarden built-in TOTP feature? I know it's a paid feature, but I think it's worth it.
  - The general idea is you keep your passwords separate from your totp. That way if one gets compromised they still can’t log in to your accounts.

- Another advantage of Ente Auth is that you can share a link with your friends, allowing them to view the OTP once without you having to send it yourself

- ## [Moved from Bitwarden in App TOTP to Ente Auth, here’s why : r/Bitwarden _202507](https://www.reddit.com/r/Bitwarden/comments/1m2in3l/moved_from_bitwarden_in_app_totp_to_ente_auth/)
  - I’m a Bitwarden Premium user, and the main reason I subscribed back in February was for the built-in TOTP feature. I've been using it regularly since then and honestly, it works flawlessly. It autofills both my passwords and TOTP codes with zero hassle.
  - But while browsing the Bitwarden community and reading up more on TOTP security, I noticed two main camps:
  1. People who are fine storing passwords and TOTP in Bitwarden.
  2. People who strongly advise separating them, using a dedicated 2FA app for TOTP.
  - I started looking at it from a hacker's perspective. What if my Bitwarden vault is compromised? If both the password and TOTP are in there, then 2FA becomes useless. It’s no longer two factors, it's just one compromised vault = full account access.
  - So I've moved all my TOTPs from Bitwarden in app TOTP to Ente Auth. I picked Ente because it syncs across devices, has end-to-end encryption, and gets regular security audits (Cure53 + Symbolic Software). Feeling a lot better now that my 2FA is stored separately.

- Seperate BW account
- You’ll need separate app for passkey, separate app for OTP, etc. I store my most important OTP on yubikey, and the rest in btw.
  - Instead of thinking about securing tokens, people should secure entire system: updates, cookies, DNS, browser extensions, regular backups, etc.

- Im opposite, im moving from Ente to Bitwarden but problem is that i cant import my codes. Bitwarden doesnt support those file types. I am using phone.
  - Open in pc the ente app and scan everythin from your bitwarden 

- Google Authenticator does not give you an easy way to export your accounts - you have to generate QR codes one by one and export that way. Ente does - you can export the vault to a json format which can be imported by Ente or other authenticatros like Aegis or 2FAS. This allows you to be safe from vendor lock-in.

- [Bitwarden Authenticator vs. Ente Auth and Alternatives for Microsoft Authenticator : r/Bitwarden _202503](https://www.reddit.com/r/Bitwarden/comments/1j3q9s4/bitwarden_authenticator_vs_ente_auth_and/)
- Microsoft's Authenticator is required for the proprietary 2FA used by some Microsoft Services
- I recently switched to Ente Auth from 2FAS but ONLY because of the available desktop app. 

- ## [Trying to move away from Microsoft Authenticator... : r/Bitwarden _202501](https://www.reddit.com/r/Bitwarden/comments/1ieedo3/trying_to_move_away_from_microsoft_authenticator/)
- Neither Bitwarden Authenticator nor Ente Auth have the MS MFA push notification feature. That is a Microsoft proprietary technology. Only MS Authenticator will do that for you.
  - I dislike MS Authenticator. It uses super duper sneaky secret closed private scary source code. It does not allow you to back up your TOTP keys to your own disk.
  - IMO Ente Auth is still a bit further ahead of Bitwarden Authenticator. It has ports to more platforms. Its cloud storage is platform agnostic.
  - If the MS push notifications are important to you, you need to keep MS Authenticator on your device. But I would recommend migrating your TOTP keys to Ente Auth.
- Bitwarden has two different TOTP functions. There is the external app, which we have been talking about, and there is also an internal function that can even assist during autofill. The internal function is effectively INSIDE your vault, so it is not suitable for unlocking Bitwarden itself. It is also somewhat controversial, with some people arguing it weakens 2FA to an unacceptable degree.

- Using MS Authenticator to login to Microsoft properties (e.g. Office 365) is a good choice. Since Microsoft controls both sides (the app and the "website"), they are not constrained by interoperability standards and can go above-and-beyond with proprietary things, such as "Push-notification with number matching". Plus, it avoids adding another entity into the security of those sites.
  - I don't like using them as a TOTP store for non-MS sites, though. Primarily because the do not have good export/import capabilities, making it hard to move away from them if they do something to lose my trust. Also not a big fan that they do not publish 3rd party security assessments and/or publish source code for ad-hoc assessments (both of which Bitwarden does).
  - My suggestion: If you have MS Authenticator installed for O365, also keep your Bitwarden TOTP in there so you have redundancy on that particular TOTP. And then keep all your TOTPs (including a second copy of Bitwarden's) in Bitwarden Password Manager, or Ente Auth -- depending on which basket you prefer -- "one well-protected basket" or "two baskets".

- I decided to use Ente instead of putting all my TOTP codes inside Bitwarden, mainly because if someone was able to access my vault, they would have all my MFA codes as well and would be able to access all of my accounts stored in BW. I now use MSA for only my work and personal Outlook accounts, and for the MFA for Bitwarden.

- I use 2FAS, and it syncs across devices. I have it installed on both my iPhone and iPad, so if I lost one device, I can still use the other device. And, you can enable it to back up to iCloud, so even if I lost both devices and got a new phone, I can restore 2FAS.

- 202605: Bitwarden now works for Office 365. https://myaccount.microsoft.com/

- ## [佬们都用的哪个2fa验证器？ - LINUX DO _202605](https://linux.do/t/topic/2250405)
- Google、Apple 的 密码也有这个功能
- 苹果自带的就非常好用，完全不需要第三方。

- 不要选微软的，迁移麻烦

- 千万别用微软的很垃圾，推荐谷歌的2fa可以云同步（自己一定要再备份一遍

- 建议找个多端同步，可以自备份的，2fa丢失比较麻烦

- aegis，自己手动导出备份到网盘
- Aegis，不过好像只支持安卓，这是个二步验证工具
- 我在用Aegis，感觉不错。开源项目，无需联网，可备份可导出可自定义图标包，可从其他软件导入。
  - 如果想要云同步且不介意隐私问题的话可以用Google的，但是强烈不推荐微软的，微软的之前做的还行，后来改版后越来越狗屎。
  - 另外，建议定期备份一下，因为一旦相关设备或者账号出问题，就只能靠所谓的恢复码了。

- 冷知识：2FA 可以同时使用多个。所以我是用的自建 vaultwarden + Authy

- 感觉谷歌的2fa挺方便的也更好迁移

- 我觉得自建bitwarden最好用，个人认为，可以自动填充完用户名和密码然后自动复制2fa码到剪贴板，特别方便
- 之前用的微软的，现在用的自建的bitwarden，自建用vaultwarden有2fa功能
- bitwarden收费吧我记得好像是
  - 可以自建vaultwarden
- [BitwardenFree计划支持L站登录了！ - LINUX DO _202604](https://linux.do/t/topic/2066874)

- 最简单的，微信小程序，腾讯身份验证器，超级方便

- ## 🔒 [怪不得没人用微软的验证器Authenticator - LINUX DO _202605](https://linux.do/t/topic/2137113)
  - 我之前还疑惑，微软的验证器Authenticator不挺好用的吗，怎么没人用呢，也没见人提，甚至许多网站的2fa设置中建议的验证器都没有提到它的名字(我用微软的authenticator，而不用谷歌的验证器的原因就是，它可以在不翻墙的情况下打开使用)
  - 然后赶紧打开Authenticator看了下，这Authenticator是不需要登录就可以使用的，所以就没有账户同步功能，数据都在本地，那万一手机丢了，那岂不是数据都没了，得赶紧备份
- 其实谷歌的不联网也可以用的，2FA本身就是个本地算法，只不过谷歌的连不上服务器同步不了会显示个加载图标有点烦
- 不止是微软，谷歌身份验证器也做的不好，有一次手滑导出时没管那个自动勾选的删除原设备记录，直接把所有的otp删了，导致我要一个个重新生成，害得我的huggingface账号灰飞烟灭

- 2FA 本身就不需要联网，另外，微软的2FA 导不出来，我又懒得一个一个改

- 自己部署，或者论坛有个公益的服务器。Bitwarden 本身E2EE 的，服务器看不了你的东西

- 现在慢慢迁移Google的身份验证器到KeepassXC，之前一直用Keepass2，迁移到XC才发现这东西真是越用越好用，纯本地，支持TOTP，ssh-agent也可以管理。

- ### [微软Authenticator丢备份 - LINUX DO _202605](https://linux.do/t/topic/2205813)
  - 我26年3月创建了备份，前天不小心手贱卸载掉了Authenticator，本想靠云备份恢复： 一查才知道，服务器出锅了（整整5天），全球都不能备份不能恢复

- 微软认证器千万不能直接登陆，要从下面点击从备份中恢复才行
  - 为了靠谱，以后可以手动两步验证添加二维码，或者双验证app，现在只能申诉了

- [Restore account credentials from Microsoft Authenticator | Microsoft Support ](https://support.microsoft.com/en-us/authenticator/restore-account-credentials-from-microsoft-authenticator)
  - You can only backup and restore on the same device type. For example, accounts backed up using an iOS device cannot be restored on an Android device.
  - android: Select either Restore from backup or Begin recovery links **before** signing in. If you have signed in, sign out before proceeding with account recovery.

- 微软Authenticator 是个大坑，apple id 都没法恢复，换手机就没了，坑死人

- 谷歌那个可以直接本地导出备份的吧？微软这个好像要root才能导出？

- Ente Auth 全平台自动备份
Aegis 手动备份
2fas 要有谷歌框架的手机才能自动备份
这三都好用

- 你这个只是自己没备份罢了，硬件passkey才叫吓人，设计本质为了安全，根本就不让你导出私钥，手机坏了就没了。
# discuss-solutions
- ## 

- ## 

- ## [Which Identity Provider are you using? : r/selfhosted _202507](https://www.reddit.com/r/selfhosted/comments/1lpvlnj/which_identity_provider_are_you_using/)
- My Authentik instance, all-in (Redis, Postgres, Server, and worker) is like 1.5G of RAM (with half being Redis) and minimal CPU usage.
  - It's configured with dozens of apps, 40+ users, and supports everything I need (LDAP, Proxy, OIDC, SAML).

- First one I tried was Authentik and loved it so never tried anything else. It works great with traefik and also supports LDAP for the couple apps I'm running that don't support anything else.

- I use Keycloak (ODIC/OAuth) + FreeIPA (LDAP). Somewhat steep learning curve, but totally worth the trouble. Those are maintained by Red Hat and pretty much set it and forget it, except for regular updates. 
  - I tried Authentik, it’s pretty good too, and easier to set up, but it feels a bit bloated. 
  - Authelia + LLDAP is perfect for low power-powered SBC (Raspberry Pi) and does not need much resources to run those.

- I choosed Authentik, as when I wanted to setup idp, authelia didn't have Ui (from what I saw) and authentik support more protocols for identification
  - it had built in reverse proxy for app not supporting idp. 
  - The cons for me is it doesn't work with haproxy for remote auth

- logto.io, adopted it and going into production soon, what sucks though is the lack of profile/account management UI components to embed into your own app. 
  - Out of the box it gives you user login/signup/password reset UI and then admin management ui, but doing user account updates is on you and it's a complicated system with too many moving parts and multiple APIs. 
  - They have something cooking regarding this, but there's no ETA nor guarantees if it will be delivered, so I'm stuck slowly building my own. 
  - Apart from that, if you don't need in-app account management, it's quite amazing and supports most if not all modern auth features.

- I consider Logto.io to be an excellent option. In fact, I’m considering the SaaS solution for a production setup, but I’ve been impressed by the UX/DX.
  - However, the FOSS is somewhat limited, in which case I also consider KeyCloak, Authentic and Authelia very good options, with each their own pros and cons.

- Authentik. Gotta be honest, I really like their partial White Labelling feature. I can put my custom wallpapers for them cool points.

- Authentik. It has a nice balance of features / size, but the documentation is not great to get started. Once you get the hang of the basic patterns for adding services, it's super simple and looks properly "branded" for a self-hosted tool.

- Authentik: for me it is easy to host, has both configuration as code, and well made UI. Has built in support for multiple types of single sign on. Also has a good track record for smooth updates.

- ## [Logto: Open-source alternative to Auth0, prettified : r/selfhosted _202208](https://www.reddit.com/r/selfhosted/comments/wmskps/logto_opensource_alternative_to_auth0_prettified/)
- Usable with ts-ocid-client (no vendor lock-in) [Not ts-ocid-client. but they have their own vanilla js client]
  - nothing is paywalled
  - No MFA yet

- [Logto: Open-source project to build sign-in experience and user identity : r/programming _202207](https://www.reddit.com/r/programming/comments/vuqtf1/logto_opensource_project_to_build_signin/)

- Why not LDAP?
  - With LDAP, every app that requires you to login handles your password to send it to the LDAP server.
  - With OIDC, you are always directed to the website of your identity provider. When it's done right, the only two things you have to trust are your browser and your identity provider.
  - Also OIDC/oauth offers many more options for handling permissions, refreshable and revocable tokens, and alternate forms of login like Device Codes.
- LDAP itself doesn't provide login, you have to integrate it manually in your app. Which isn't too bad, but you're better off using a sso provider that connects to LDAP.

- What is it that makes your solution better than keycloak?
  - Logto also offers a bunch of useful SDKs out of the box, including native SDKs such as kotlin for Android and Swift for iOS.
  - another thing I can think of is that Logto provides a great user experience in the admin console. The interactive SDK integration guide and the sign-in experience customization page look really interesting. 
- Our highlight is not about how many techniques we're using (we'll support more 3rd party services though), it is about the smooth and unified user experience, and how easy you can build your user identity from frontend to backend with a standard and secure implementation.

- [Logto: A cost-effective open-source alternative to Auth0 : r/coolgithubprojects _202303](https://www.reddit.com/r/coolgithubprojects/comments/11hnspm/logto_a_costeffective_opensource_alternative_to/)
- Is this similar to authentik?
  - as a heavy Authentik user I read through the docs and I think this solution is somewhere inbetween something like Authelia and Authentik.
  - It has a built in IdP, looks very straightforward to setup and is fairly customizable/extensible, but not nearly as much so as Authentik in most areas.
  - I fully plan to spin this up in my test environment to kick the tires, but my initial thought is that this aims at being more targeted towards developers looking for a straightforward drop-in auth provider for their app.

- Really a great project look awsm, but lacks few important features like having custom clientId and secret, i couldn't edit it from db directly bcz of 21 char limit.

- ## [Authentik or Authelia: Attack Surface & Disclosed Vulnerabilities : r/selfhosted _202509](https://www.reddit.com/r/selfhosted/comments/1nbnznf/authentik_or_authelia_attack_surface_disclosed/)
- Since Authelia hasn't undergone an audit you can't really compare them.
  - Looking at Authentik in isolation, it's obviously good that they had the audits and that the vulnerabilities were fixed. 
  - You have to keep in mind that these are identity platforms first and authentication second. If you can, use a hard access check: VPN, SSH, mTLS, or IP whitelists.
  - Secondary measures can also be good: keys in custom HTTP headers, basic auth (enforced by the reverse proxy, not by 3rd party apps), country geo-blocking (whitelisting, not blacklisting!) can be good.

- ## [Authentik, Authelia, Zitadel, PocketID, Caddy/Traefik : r/selfhosted _202503](https://www.reddit.com/r/selfhosted/comments/1jdg374/authentik_authelia_zitadel_pocketid_caddytraefik/)
  - I do not mind Authentik's RAM usage if I get simplicity. 8 GB of additional RAM is cheaper than another hour spend configuring.

- Authentik's outposts make it compatible with basically anything. It's the gold standard of self-hosting SSO. Since turning into a business, the developer's done the opposite of enshittify it, turning enterprise features into FOSS features.

- I’m running Authelia atm (with lldap as LDAP backend), it’s pretty lightweight, all of the config is yaml-based though (can be an up- or downside depending on your preferences)
  - Authentik is somewhat harder to wrap your head around at the beginning, but is an all-in-one solution with more features than Authelia (supports advanced stuff if you care about stuff like e.g. simple onboarding)
  - PocketID looks like an amazing solution, but keep in mind it only supports passkeys via OIDC, which excludes services like Jellyfin which only really support LDAP

- ## [Authelia/Authentik comparison : r/selfhosted _202502](https://www.reddit.com/r/selfhosted/comments/1ije2ag/autheliaauthentik_comparison/)
- If you prefer configuration using yaml then authelia would be better for you, 
  - if you prefer doing stuff via the ui then I think authentik would be better. 
  - That's one thing I've found out when researching both, I use authentik myself because I prefer the UI

- My four Authentik containers hover around 900-1000MB on average. Not too uncommon for complex containers, but not the smallest on my system either. 

- Authentik can do everything Authelia can and has a nice GUI. Seems like an easy win to me. But that's just my 2c.

- ## [Authentik and Authelia does it matter ? : r/selfhosted _202401](https://www.reddit.com/r/selfhosted/comments/191879o/authentik_and_authelia_does_it_matter/)
- Depends on your goals to accomplish.
  - Usually, SSO rollout makes sense if there are many end users accessing services and you want to streamline the onboarding process as well as management of those users. Here, keycloak and authentik are good choices, as they support various protocols to sync and do the auth flows (LDAP, OIDC, SAML etc.).
  - However, to really make use of it you would typically run some form of directory service (Active Directory, LLDAP, Azure AD) to manage your users, which are then using the IdP to proof their identify and access services.
  - Note though, that your proxied services must support SSO too. Otherwise, you just have another auth layer in front of the authentication scheme of the proxied service. So you would authenticate via Authentik/Authelia/Keycloak and then also have to login into the actual application again with new creds as no SSO is supported.
  - If you are the single user of your services, then using the normal username + password logins may be easier then setting up SSO and configuring all corresponding applications for it. Also, as most selfhosted apps do not support SSO.
  - Authelia + LLDAP do not allow for password resets by the users itself. So if you plan to have many users, better use Authentik or Keycloak.
  - I recommend starting with Authelia and see how it runs and works with your setup and apps.

- I use Authentik for my office and home lab authentication. Authentik / Keyclock does have a lot of features when compared to Authelia . Try everything and pick whichever fits your needs .

- Having used both, authentik is better, authelia is easier.

- ## [Authelia vs Authentik : r/selfhosted _202110](https://www.reddit.com/r/selfhosted/comments/q721e9/authelia_vs_authentik/)
- if you like GUI go with authentik, or you don’t mind tinkering with config.yml then authilia is another good choice. My only gripe with Authentik is their documentation that only scratches the surface but it can do a lot more such as bypass, proxying, third-party integration with ReCaptcha, duo security, etc.

- ## [Authelia vs Casdoor : r/selfhosted _202301](https://www.reddit.com/r/selfhosted/comments/10kwn1b/authelia_vs_casdoor/)
- Authentik (using Python) can occupy 700MB of memory (or more) just for idling around while Authelia can use less than 30MB while idling. 
  - And the Authentik documentation is even recommending 2GB to be on the safe side (because you're not always just idling and there's actually some work to do when authenticating). 
  - But you're right, Authelia can use a lot of resources with the file-based user database and Argon2 algorithm when authenticating (which you were probably referring to, I guess).
  - I'm using LLDAP for user management, though (which uses 20MB or so) and using roughly 50MB for the same task where Authentik uses at least 700MB is a significant difference, isn't it?

- Regarding Casdoor, it might be a good idea to use it if you're just quickly prototyping an application. However, if you intend to use it in a production environment, you'll be taking on a significant security risk.
  - As a SCIM, Casdoor offers almost no auditable security features. Furthermore, the developers of this project tend to conceal security issues and quietly patch them instead of handling problems publicly, transparently, and informing users.
  - A real-world example is that prior to version 1.811.0, Casdoor had a security vulnerability that allowed anyone to create users without authorization.
  - The developers' response was to quietly merge a patch and pretend the issue didn't exist. You won't find any disclosure about this vulnerability within the Casdoor project itself. I only became aware of this problem after discovering that "oas.fun" was exploiting this vulnerability to create numerous users on my instance.

- Zitadel, Casdoor and Authentik are all great, and each have their use-cases in my opinion, but among the options Authelia seems to be made for personal servers.
  - Authelia uses LDAP as its backend for users. Or files, but the LDAP backend is the reason I went with Authelia. What I found is that a lot of selfhosted apps still don't support OIDC, let alone SAML which was kind of a weird in-between solution that didn't get much adoption in this space, but LDAP is still quite popular. In particular Jellyfin which has a first-party LDAP plugin.
  - Their docs also provide lots of information on integrations with Gitea, Grafana, Traefik, etc. which are the apps I deployed, so it was perfect to work with.

- Casdoor has lots of hidden feature that you need to ask the team, they are responsive but not quite friendly, and some must go through customer support.
- Authelia is only act as SSO portal, there is no functionality regarding ORG/User management. This is to compare with Zitadel. However, Authelia has crowded community since it's existing for quite a long time.

- ## [Golang Auth Dilemma: Clerk vs SuperTokens vs DIY  : r/golang _202409](https://www.reddit.com/r/golang/comments/1ff8nlz/golang_auth_dilemma_clerk_vs_supertokens_vs_diy/)
- I would consider a proper OIDC auth platform. Personally I’d choose keycloak. It can take a little fiddling with to get a production instance up but once you figure it out, everything just works. 
  - Plus it implements the login on the authorization server vs custom implementation client side which is what clerk and supertokens offer. So if you have multiple clients you don’t need a separate implementation for each client. 

- I’ve tested Supertokens in a side project and I didn’t have a good experience. I’ve tried to use a custom UI at first, but the lack of documentation discouraged me. 
  - I’m testing Zitadel now, and it’s working well so far. They have a SDK for Go and also for React. I like the documentation and all the features they offer, it seems a really complete project. And on top of that they have a self host option well documented, even with more advanced examples like a setup with a reverse proxy. Other aspect is that their SDK’s seems really well written and small (most frontend stuff is a wrapper on top of a OIDC library). When I dig through the Supertokens for React, it seemed really bloated and confuse to me.

- I used clerk in 2 different project both with go backends and react frontends, I have to say it’s pretty nice they have both a simple sdk that’s basically plug and play and a detailed api so you can implant things on your own more deeply. Highly recommend them

- I chose to do a DIY JWT issuer that integrates with our existing LDAP. It uses asymmetric certificates to sign the JWTs that applications can verify. Applications just need to keep a current public cert to verify tokens. The source is at https://github.com/hppr-dev/stoke-auth .
  - The main reason I chose DIY was our existing infrastructure. I had considered keycloak, but I wanted something a bit more streamlined that would make sense being deployed with the application or independently. As for other cloud based solutions, a SaaS product would probably be a hard sell. I do think that DIY takes more work (obviously) but I felt many solutions out there either offer too much or too little.

- ## [Best self hosted authentication solution? : r/selfhosted _202408](https://www.reddit.com/r/selfhosted/comments/1eohsds/best_self_hosted_authentication_solution/)
- I had authelia running but it was a nightmare with way too many config file settings, environment variables, and nginx proxy configurations. 

- If resources matter: KanIDM
  - Authelia is not as usability friendly as Authentik, but uses more resources and has less features than KanIDM
  - Keycloak is more complicated than Authentik and uses more resources than KanIDM
  - LLDAP supports LDAP only while KanIDM supports LDAP, OIDC, RADIUS, SSH etc and it even has a user self service UI

- Authelia: Doesn’t really have an UI though.
  - Authelia without UI is easier to use than authenthik with UI

- Happy with authelia here, but there's no admin gui... which to my mind removes a risk, but makes initial setup harder. But like most tool of this ilk, once it's set up you don't really need to touch it

- ## [What SSO to choose? : r/selfhosted _202503](https://www.reddit.com/r/selfhosted/comments/1jk1v2x/what_sso_to_choose/)
- Authentik free tier allows social login. I have log in with google and other sources on my homelab

- I tried Authentik, but it was too heavy and too complex for usage. I love Authelia since. Very light, efficient and powerful. I recommend.

- The way Authentik handles filtering and policies is pretty awesome because it's basically just Python. Which means you can do silly things with access policies for users, provided you can write the Python script.

- Authelia is really lightweight, but everything is done with config file, and that's quite annoying for me, but it might be worth it 
  - Authentik is more resources intensive (around 1GB of Ram minimum at all time) , but it's not that hard to use, nice UI, and it's a very very powerful tool, you can really customise it a lot 
  - Keycloak and zitadel are more difficult to use, and not as powerful as authentik 
- I love authelia exactly for that. When I have to setup all my services from scratch (for whatever reason) I don't have to go through all the GUI stuff again and everything works as before.
- Zitadel requires manually using webgui or apis to configure environment. Authelia offers a config file

- If you need SAML and full control, go with Keycloak it’s powerful but a bit complex. For something simpler that focuses on modern OIDC use cases, Zitadel is lighter and easier to set up.

- [Should I build a simple Auth service in GO instead of Keycloak/Authentik? : r/golang](https://www.reddit.com/r/golang/comments/1jsqdnq/should_i_build_a_simple_auth_service_in_go/)
  - If you don't need multi-tenancy, try Ory

- ## [Keycloak vs Authentik : r/selfhosted _202502](https://www.reddit.com/r/selfhosted/comments/1j04p6x/keycloak_vs_authentik/)
- I have keycloak at home, it was a massive pain to get right and the learning curve was a vertical wall. But it's an enterprise grade solution, I'm so glad I did it.
  - Same here. I used both and settled on Keycloak due to its stability and code maturity. Nothing wrong with Authenik, it just needs more time to polish out to match the maturity of Keycloak.

- I’m using Authelia with Lldap auth and nginx reverse-proxy. Easy to setup, lightweight solution.
  - From authelia.com: "With a compressed container size of less than 20 megabytes and observed memory usage generally below 30 megabytes."
  - My own experience is the same. The configuration is a simple static yaml file that you can easily replicate to additional nodes.
- Mine runs on .05% cpu utilization and 50mb of ram

- Authelia is great they just haven't progressed on their roadmap in over a year, while their competitors and the wider oidc spec have both moved forward.

- My setup currently is with Authelia + file based user configuration (it supports LDAP as well) + Caddy for reverse proxy, it's working great and has a lower memory footprint.

- Authentik is much easier to maintain while still providing all functionality we need. Of course, keycloak can do more, but we simply don’t need that.

- I chose Authentik because it supports passwordless login flows

- Authentik is pretty resource intensive for what it is

- ## [What are people using for authentication in late 2024? : r/selfhosted _202409](https://www.reddit.com/r/selfhosted/comments/1fnn6fp/what_are_people_using_for_authentication_in_late/)
- Can't go wrong with Authentik. SSO, SAML, ODIC, Radius, LDAP. You name it, it does it.
  - It also either works with proxyAuth (nginx/traefik will "ask" authentik if the user is authorized, without everything being proxied through authentik).
  - And- if all else fails, it supports proxy mode, where it will fully proxy the given application, and wrap auth around it.

- I also use authelia. Overall happy with it but it has a fairly slow development and it seems like there’s mostly one guy doing all the work.

- I am using Keycloak as it’s backed by Red Hat, so it gives me some additional assurance of its longevity

- Keycloak, because Authentik just doesn’t support many features that I want to use like Kerberos.

- Tried oidc recently with Authelia (was using it with forward-auth so far), found it pretty easy to implement actually
  - Authentik is certainly simpler and easier to use, authelia is based on a text configuration and it's more work, but straightfoward once you have something to copy and paste for different apps

- Can you use Authentik without reverse proxy, so just locally? I'm not really planning to expose anything.
  - You can use a reverse proxy locally without exposing any ports and even get domain names and ssl certs.

- Authelia but I was finding OIDC too difficult so have Authentik for that. Probably will switch to Authentik completely sometime soon. LDAP backend for both.

- ## [Keycloak vs. Authentik vs. Authelia, help choose SSO : r/selfhosted _202305](https://www.reddit.com/r/selfhosted/comments/13rr6i7/keycloak_vs_authentik_vs_authelia_help_choose_sso/)
  - Authentik has everything. You're going to find all your apps have spotty/different auth methods, and that's what makes authentik great because it'll adapt to whatever auth. LDAP? Authentik has it. SSO? Authentik has it. None? Authentik will auth via reverse proxy.

- I prefer Authelia because it's just a config file with a bunch of secrets. So much simpler and easier to manage. 
- Something to add: Authelia is significant faster than Authentik.

- I’ve been using Authelia for the better part of 2 years and really really like it. It is definitely not the most beginner friendly without a GUI but the docs are clear and easy to follow.
  - I have nothing against Authentik, but I tried it last year and didn’t think it was robust enough with features. That may have since changed. The UI is really nice.

- I see a lot of votes for Authentik, but as far as i've seen there hasn't been an audit for it?
  - And also what was said today about the issue with LDAP that still isn't fixed, I'm wondering why still a lot of people vote for it
- If you have seen the issues with KeyCloak, you wouldn't like that either.

- I would recommend another one: Casdoor written in Go. 
  - I have used Authelia and it uses a lot more reousrces and Casdoor, which is small but packed with features.

- I got tempted to use casdoor for its nice WebAuthn options, in which authelia is very lacking (non-exists). Just tried my best to run casdoor in docker with sqlite as db driver, it did not work. Documentation did not help much either.

- How much resources does Casdoor use? On the systems that I know Authelia and LLDAP use less than 100 MB RAM alltogether hence I'm curious how much Casdoor might be able to save then.
  - When idle: 0.13 vCPU, 12.66 MiB

- I am using Authentik. I can recommend it. It's complex but I would argue that Keycloak is even more complex and Authelia is not complex enough.

- Keycloak has the upside of being under the stewardship of Red Hat.

- Over the years I have run all three. I started with Authelia. It was good but didn't have many features. I then added Keycloak but it was very difficult to upgrade when new versions came out. Then once Authentik matured I started migrating to it. I do like Keycloak is very light and can run on sqlite where Authentik requires a whole stack. I currently no longer run Authelia. I migrated all Authelia stuff to Authentik. I do still have keycloak because configuring apps for SAML can be very difficult so I haven't gone back to all of them and moved them to Authentik.

- I personally use Authentik backed by FreeIPA. FreeIPA is where I have my canonical set of users/groups and works for stuff that can only use LDAP/Kerberos. Authentik pulls users/groups from FreeIPA for OIDC and proxy auth flows set up in Nginx Proxy Manager.

- ## [Lightweight keycloak alternative : r/selfhosted _202305](https://www.reddit.com/r/selfhosted/comments/13sa28x/lightweight_keycloak_alternative/)
- I'm using Authelia, with https://github.com/lldap/lldap as backend to create and store users.

- authentik 1 user used ~500MB RAM
  - authelia ~30-50MB RAM but no web UI for users to manage their own info
  - casdoor at least 100MB memory
  - ZITADEL consumes around 512MB Ram

- I’ve recently set up Caddy Security (or authp) and was impressed. Much easier to set up than Authelia and does more.

- ## [Open source alternative to Keycloak and Ory for user auth _202110](https://www.reddit.com/r/golang/comments/q3zg70/open_source_alternative_to_keycloak_and_ory_for/)
  - SuperTokens.io recently launched our Go SDK for user auth.
  - https://github.com/supertokens/supertokens-core /202509/java
  - license: apache2 + EE

- Does casbin do Oidc and SSO ?
  - If you want Oidc and SSO, you should consider to use Dex.

- ## [Stateless alternative to Keycloak? : r/selfhosted _202105](https://www.reddit.com/r/selfhosted/comments/n8jhxu/stateless_alternative_to_keycloak/)
  - it seems like Keycloak maintains its own internal in-memory Infinispan cluster, which means the various instances of Keycloak container have to be coordinated together AND since each container stores state, it’s much less feasible to randomly spin up/spin down containers since it’ll cause a large disruption in signouts.

- You can run Keycloak in cluster mode, where the infinispan cache is clustered, allowing for new nodes to join, and leave, the cluster without disruption.

- Authelia uses Redis.
  - Authentik uses Redis and Postgres.

- Authelia by itself cannot work as OIDC provider, which scratches it off my list.
  - Authelia version 4.29.0 added beta support for OIDC 
# discuss-rbac/permissions
- ## 

- ## 

- ## 

- ## [Any recommendations for Open Source RBAC? : r/devops _202501](https://www.reddit.com/r/devops/comments/1hsq81f/any_recommendations_for_open_source_rbac/)
  - Each Role has different permissions (View, Edit, Delete)

- In order of preference
  - OpenFGA
  - OpenPolicyAgent
  - Casbin
  - Roll your own

- As you've seen open source system RBAC systems do exist, but as you've probably also noticed they tend to get complex quickly becuase they are designed a generic solution for every RBAC scenario. Take a moment to decide how fine grained you need to get.
  - If it's just "User with Role X can List resource type Y", roll your own.

- Keycloak has rbac built in no? Its a full AAA solution. Authenticate Authorize Audit.

- Sadly, all the allegedly RBAC libs I found some years ago were either hugely overcomplicated or didn't even support nested roles. It was frustrating. I rolled my own.

- LDAP is a data store. You can define your roles there but it lacks the Access Control part.

- For RBAC implementation, I'd strongly recommend looking into Casbin (https://casbin.org/). 
  - It's a mature, widely-adopted open source authorization library that integrates well with Keycloak and provides exactly what you're looking for out of the box. 
  - It supports fine-grained RBAC with custom permissions, has adapters for multiple databases, and includes a management UI called Casdoor that can save you significant development time. 
  - The learning curve is reasonable, and there's excellent documentation and community support.

- RBAC for what? The app, or for other apps? For your directory? I'm not understanding what you're trying to build RBAC on top of.

- Have you heard of the Ory stack https://ory.sh

- We had a similar problem at my company. Used Keycloak for authentication only, but implemented RBAC in our Postgres database. Tried casbin, but it's not flexible enough.
# discuss
- ## 

- ## 

- ## 

- ## 
