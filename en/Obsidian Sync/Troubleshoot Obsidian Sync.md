---
cssClasses: soft-embed
---

This page lists common issues that you might encounter with [[Introduction to Obsidian Sync|Obsidian Sync]], and how to address them.

![[Sync your notes across devices#^sync-files-on-demand]]

## General

### Conflict resolution

A conflict happens when you make changes to the same note on two or more devices between syncs. For example, you might have changed a note on your computer, and before that change is uploaded, you also change the same note on your phone.

Conflicts usually happen more frequently if you work offline, since there are more changes and a longer period of time between syncs and thus more potential conflicts.

When Sync downloads a new version of a note, and finds that there are conflicts with the local version, the changes are merged with Google's [diff-match-patch](https://github.com/google/diff-match-patch) algorithm.

For conflicts in Obsidian settings, such as plugin settings, the process is a different. Obsidian Sync will merge the JSON files, by loading the local JSON and the remote JSON. Then Sync will apply the keys from the local JSON on top of the remote JSON.

> [!help] To find when conflicts have happened, you can search for "Merging conflicted file" in **Settings → Sync → Sync activity → View**.

### Obsidian Sync deleted a note I just created on two devices

Generally, Obsidian Sync tries to [[#Conflict resolution|resolve conflicts]] between devices by merging the content of the conflicting notes. Unfortunately, merging conflicting notes can cause issues for users who *automatically generate* or *alter notes* on startup, for example using [[Daily notes]].

If a note was created locally on a device less than a couple of minutes before Sync downloads a remote version of that note, then Sync keeps the remote version without attempting to merge the two. You can still recover the local version using [[File recovery]].

### Obsidian Sync will not Sync my plugins and settings updates

Obsidian [[Sync limitations#Does Obsidian Sync live-reload my settings?|does not live-reload settings]]. You will need to restart Obsidian on the other devices after they have updated their settings. On mobile devices, this may require a force-quit of Obsidian.

> [!example]- Example: Changing a theme
> - Your primary device, a computer, currently has a custom theme and you decide to change it back to the default theme.
> - You confirm in the Sync log that the files have been sent to the remote vault. However, your open mobile device, still reflects your custom theme.
> - You open the Sync log on the mobile device, and confirm that you have received an updated `appearance.json`.
> - You restart Obsidian on the mobile device.
> - Once re-opened, the mobile device should reflect the same theme as your primary device. 

### My files keep disappearing from Sync

> [!hint] On Windows, Windows Defender might quarantine files with codeblocks in notes, causing specific notes to disappear.

![[Migrate to Obsidian Sync#Moving your vault out of a third-party syncing service]]

## Account

### What does "Vault limit exceeded" mean?

Your account exceeds the [[Sync limitations#How large can each remote vault be|maximum storage size]]. See [[Plans and storage limits]].

Since attachments and version history contributes to the total size of your vault, your vault can exceed the maximum size even if the actual size of your vault is less than the limit.

To identify and purge large files from the vault:

1. Open **Settings → Sync**.
2. Explore the options under **Vault size over limit** for how you can reduce the size of your vault.

### What does "Vault not found" mean?

`{"res":"err","msg":"Vault not found."}`

This error may occur in the following scenarios:

1. The vault has been deleted from another device for any reason.
2. The sync subscription was inactive for over 30 days, leading to the removal of the remote vault.
3. The subscription was canceled or refunded, resulting in the purging of the remote vault.

In each case, it is necessary to [[Set up Obsidian Sync#Disconnect from a remote vault|disconnect from the remote vault]] and [[Set up Obsidian Sync#Create a new remote vault|create a new remote vault]], ensuring the data on your device is retained.

## Android

### My phone is deleting my attachments I receive through Sync

This issue is likely caused by Google Photos managing these attachments. To prevent the operating system from altering the attachments you receive, add a `.nomedia` [file to your vault](https://www.lifewire.com/nomedia-file-4172882) on your Android device.

> [!tip] A community plugin, [Android Nomedia](https://obsidian.md/plugins?id=android-nomedia), simplifies this process. Install and use this plugin on your Android phone, as the `.nomedia` file will not be synced across devices with Obsidian Sync.
