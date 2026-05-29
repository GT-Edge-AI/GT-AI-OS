# Sharing Agents

This guide explains how to share your agents with team members and across your organization.

## Visibility Levels

| Visibility | Who Can Access | Best For |
|------------|----------------|----------|
| Individual | Only you | Personal agents, development |
| Team | Selected team members | Team-specific workflows |
| Organization | All users in your organization | Company-wide tools |

**Note**: Only Tenant Admins can set visibility to Organization. All users can access Organization-level agents.

## Sharing with Teams

### Setting Team Visibility

1. Edit your agent
2. Change visibility to **Team**
3. Select which teams should have access
4. Save changes

### Team Member Access

Team members can:
- Use the agent in chat
- View agent details
- See it in their agent gallery

### Revoking Team Access

1. Edit the agent
2. Deselect teams or change visibility
3. Save changes

## Sharing Organization-Wide

### Setting Organization Visibility

**Note**: Only Tenant Admins can set Organization visibility.

1. Edit your agent
2. Change visibility to **Organization**
3. Save changes

All organization members can now access the agent.

### Considerations for Organization Agents

- Ensure the agent is well-tested
- Write clear documentation
- Consider the broad audience
- May require Tenant Admin approval

## Export and Import

### Exporting for Sharing

Export agent configuration to share with colleagues or backup:
1. Go to the Agents page
2. Select agent(s) to export, or use the menu on a single agent
3. Click **Export**
4. A CSV file downloads (or ZIP for multiple agents)
5. Share the file

### Importing Shared Agents

Import an agent configuration file:
1. Go to the Agents page
2. Click **Import**
3. Upload the CSV file or paste CSV text directly
4. Review the agents that will be created
5. Click **Import**

**Note:** Datasets are matched by name. Ensure matching dataset names exist in your instance for full functionality.

## Best Practices

### Before Sharing

1. **Test thoroughly**: Verify behavior is consistent
2. **Document well**: Write clear descriptions
3. **Set appropriate visibility**: Don't over-share
4. **Consider security**: Don't expose sensitive prompts

### When Sharing

1. **Communicate**: Let users know about the agent
2. **Provide guidance**: Share tips for best use
3. **Set expectations**: Explain what the agent can/can't do
4. **Gather feedback**: Improve based on user input

### After Sharing

1. **Monitor usage**: Check if it's being used effectively
2. **Update as needed**: Keep the agent current
3. **Respond to feedback**: Address issues promptly
4. **Delete if unused**: Remove outdated agents

## Troubleshooting

### Users Can't See Shared Agent

- Verify visibility settings
- Check that users are in the correct team
- Ensure the agent is active (not deleted)

### Permission Issues

- Check organization policies
- Contact your Tenant Admin
