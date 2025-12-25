# Netcoin Documentation

Official documentation for the Netcoin blockchain project, built with MkDocs and Material theme.

## 📚 Live Documentation

**🌐 [View Live Docs](https://netcoin-ntc.github.io/netcoin-docs)**

The documentation is automatically deployed to GitHub Pages on every push to the `main` branch.

## 🏗️ Documentation Structure

```
docs/
├── index.md           # Landing page
├── OVERVIEW.md        # Project overview and philosophy
├── FEATURES.md        # Feature descriptions
├── CLI.md            # Command-line interface reference
├── ARCHITECTURE.md   # Technical architecture
└── ROADMAP.md        # Development roadmap

mkdocs.yml           # MkDocs configuration
.github/
└── workflows/
    └── deploy.yml   # GitHub Actions deployment
```

## 🚀 Development

### Local Development

1. **Install dependencies**:
   ```bash
   pip install mkdocs-material mkdocs-git-revision-date-localized-plugin pymdown-extensions
   ```

2. **Serve locally**:
   ```bash
   mkdocs serve
   ```
   Visit `http://localhost:8000` to preview changes.

3. **Build for production**:
   ```bash
   mkdocs build --clean
   ```

### Making Changes

1. **Create/edit documentation** in the `docs/` directory
2. **Test locally** with `mkdocs serve`
3. **Commit and push** to deploy automatically

### Content Guidelines

- Use **Markdown** for all documentation
- Follow the existing **structure and style**
- Include **code examples** where helpful
- Keep content **concise and clear**
- Use **relative links** for internal references

## 🔧 Technical Details

### MkDocs Configuration

- **Theme**: Material Design
- **Features**: Search, navigation, code highlighting
- **Plugins**: Git revision dates, table of contents
- **Extensions**: Admonitions, details, tabs, superfences

### CI/CD Pipeline

- **Trigger**: Push to `main` branch
- **Build**: Python 3.x with MkDocs
- **Deploy**: GitHub Pages via Actions
- **URL**: `https://netcoin-ntc.github.io/netcoin-docs`

## 📝 Contributing

### For Documentation Updates

1. **Fork** this repository
2. **Create a feature branch**: `git checkout -b docs/update-feature`
3. **Make changes** to files in `docs/` directory
4. **Test locally**: `mkdocs serve`
5. **Commit changes**: `git commit -m "Update documentation for feature"`
6. **Push and create PR**

### For Technical Documentation

- Use **code blocks** with syntax highlighting
- Include **diagrams** where helpful (Mermaid support)
- Keep **API references** up to date
- Document **breaking changes** clearly

## 📋 Repository Maintenance

### Regular Tasks

- **Update dependencies** in CI/CD pipeline
- **Review and merge** documentation PRs
- **Archive old versions** when major releases occur
- **Update links** after repository restructuring

### Versioning

Documentation follows semantic versioning aligned with Netcoin releases:
- **Major**: Breaking changes or redesigns
- **Minor**: New features or significant updates
- **Patch**: Corrections and small improvements

## 🆘 Troubleshooting

### Common Issues

**"docs_dir not found"**
- Ensure files are in `docs/` directory, not root
- Check `mkdocs.yml` configuration

**"Build fails in CI"**
- Test locally first: `mkdocs build --clean`
- Check for broken links or syntax errors

**"Pages not updating"**
- Wait 2-3 minutes after successful workflow
- Check repository Pages settings
- Verify workflow permissions

### Getting Help

- **Issues**: Report bugs in this repository
- **Discussions**: General questions in [community repo](../community)
- **Technical**: Post in Netcoin development channels

## 📄 License

This documentation is part of the Netcoin project and follows the same license terms.

---

*Contributing to documentation helps make Netcoin more accessible to everyone!* 📚✨
