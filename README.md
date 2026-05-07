# Project Org Clone

Local clone of the **ORG-UNAZ22191C091** SharePoint site, decoupled from the live
OneDrive sync for stable offline access.

## Source

SharePoint URL: `https://uniwa.sharepoint.com/sites/ORG-UNAZ22191C091/`

Local OneDrive sync folder: `C:\Users\00060951\UWA\<site-display-name> - Documents`

> Update the path above once the OneDrive sync is confirmed and the folder name is known.

## Destination

`C:\Users\00060951\Project_Org_Clone`

## How It Works

The sync script (`sp_clone.py`) in the sibling project
`C:\Users\00060951\Project_Sharepoint_Clone\` is called with explicit `--source` and
`--dest` arguments. It performs incremental copies using a JSON manifest of file
timestamps -- only new or modified files are copied.

## Usage

Run manually:

```powershell
python "C:\Users\00060951\Project_Sharepoint_Clone\sp_clone.py" `
    --source "C:\Users\00060951\UWA\<site-display-name> - Documents" `
    --dest "C:\Users\00060951\Project_Org_Clone"
```

## Scheduling

Windows Task Scheduler task: **SharePoint Org Sync**

Runs daily at 05:00 AWST.

```powershell
# Check status
Get-ScheduledTaskInfo -TaskName "SharePoint Org Sync"

# Run manually
Start-ScheduledTask -TaskName "SharePoint Org Sync"

# Disable
Disable-ScheduledTask -TaskName "SharePoint Org Sync"
```

## Output

- `sync_manifest.json` -- per-file metadata for change detection (not tracked in git)
- `logs/sync_YYYY-MM-DD_HHMMSS.log` -- timestamped run logs (not tracked in git)

## Related

- Sibling project (PWA-IT-2020 site): `C:\Users\00060951\Project_Sharepoint_Clone`
- Sync script: `C:\Users\00060951\Project_Sharepoint_Clone\sp_clone.py`
