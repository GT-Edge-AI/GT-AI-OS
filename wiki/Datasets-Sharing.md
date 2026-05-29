# Sharing Datasets

This guide explains how to share datasets with team members, across your organization, and how to export/import datasets.

## Visibility Levels

| Visibility | Who Can Access | Best For |
|------------|----------------|----------|
| Individual | Only you | Personal knowledge bases |
| Team | Selected team members | Team-specific resources |
| Organization | All users in your organization | Company-wide knowledge |

**Note**: Only Tenant Admins can set visibility to Organization. All users can access Organization-level datasets.

## Setting Visibility

### Changing Dataset Visibility

1. Open the dataset details page
2. Click **Edit** or access settings
3. Change the visibility setting
4. Select teams (if Team visibility)
5. Save changes

## Sharing with Teams

### Team Access

When you share with a team:
- Team members see the dataset in their list
- They can use it with their agents
- They can view document contents

### Selecting Teams

1. Set visibility to **Team**
2. Select which teams should have access
3. Save changes

### Revoking Access

1. Edit the dataset
2. Deselect teams or change visibility to Individual
3. Save changes

## Organization-Wide Sharing

### Making Datasets Organization-Wide

1. Edit the dataset
2. Set visibility to **Organization**
3. Save changes

All organization members can now access the dataset.

### Considerations

Before sharing organization-wide:
- Ensure content is appropriate for all users
- Verify data sensitivity is acceptable
- Document what the dataset contains
- Consider maintenance responsibilities

## Export and Import

### Exporting Datasets

Export datasets for backup or transfer to another GT AI OS instance:

1. Go to the **Datasets** page
2. Select one or more datasets using checkboxes
3. Click **Export**
4. A ZIP file downloads

**Export contents:**
- **metadata.json**: Dataset name, description, category, tags, and settings
- **documents.json**: List of uploaded documents with their metadata
- **chunks.jsonl**: Processed text chunks used for search

**Note**: Maximum export size is 100MB.

### Importing Datasets

Import previously exported datasets:

1. Go to the **Datasets** page
2. Click **Import**
3. Select the ZIP file
4. Review the configuration and any warnings
5. Choose whether to **re-process chunks**
6. Click **Import**

**Re-processing chunks:** When moving datasets between different GT AI OS instances or versions, it's recommended to re-process the chunks. This ensures optimal search quality with the current embedding model. If you're restoring a backup to the same instance, you can skip re-processing.

### Export and Delete Operations

Export and delete actions work for both individual datasets and bulk selections:

**Single dataset:**
- Click on a dataset, then use the **Export** or **Delete** button

**Multiple datasets:**
- Select datasets using checkboxes on dataset cards
- Click **Export** to download all selected as a ZIP
- Click **Delete** to remove all selected (with confirmation)

## Best Practices

### Before Sharing

1. **Review content**: Ensure accuracy and appropriateness
2. **Document purpose**: Write clear descriptions
3. **Set proper visibility**: Don't over-share
4. **Add relevant tags**: Help others find the dataset

### Managing Shared Datasets

1. **Communicate changes**: Let users know about updates
2. **Version carefully**: Major changes may affect agents using the dataset
3. **Monitor usage**: Check if dataset is being used effectively
4. **Delete when outdated**: Remove stale content

### Security Considerations

- Don't share sensitive information inappropriately
- Review content before organization-wide sharing
- Consider access controls for sensitive data
- Follow your organization's data policies

## Troubleshooting

### Users Can't See Shared Dataset

- Verify visibility settings are correct
- Confirm users are in the selected team(s)
- Check that the dataset is active

### Access Permission Issues

- Review your sharing settings
- Ensure you have permission to share
- Contact your Tenant Admin if needed

### Import Warnings

If you see warnings during import:
- **Missing embedding model**: Re-process chunks recommended
- **Large file size**: May take longer to process
- **Duplicate names**: Consider renaming before import
