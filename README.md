**You are NOT supposed to push to this repo.** 


The data flow is as below. 

`klaytn-docs:master` -> `Crowdin` -> `klaytn-docs:l10n`

- If you want to change the source content, you should update the `master` branch of `klaytn-docs`.
- If you want to change the translation, you should work on [Crowdin](https://crowdin.com/project/klaytn-docs). Then the modified translation will be pushed back to the `l10n` branch of `klaytn-docs`. To request access to the translation, follow the link - https://crwd.in/klaytn-docs. 
- Do NOT push to `klaytn-docs:l10n` directly. It will be overwritten by Crowdin and the change will get lost.

`dev` branch of this repo mirrors the `ko/docs` subfolder of the `klaytn-docs:l10n` periodically. Approved contents will be merged to `master` branch and published at https://ko.docs.klaytn.com. 

