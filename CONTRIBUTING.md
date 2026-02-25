# 🤝 DARSHAN EASE - Contributing Guide

> Guidelines for contributing to DARSHAN EASE

---

## 🎯 Welcome Contributors!

Thank you for your interest in contributing to DARSHAN EASE! We welcome contributions from everyone. Whether you're a developer, designer, or enthusiast, there are many ways to help.

---

## 📋 Before You Start

1. **Read the Project**: Understand the project's goals and structure
2. **Check Documentation**: Read [README.md](README.md) and [FEATURES.md](FEATURES.md)
3. **Review Existing Issues**: Check if your contribution is already in progress
4. **Respect Community**: Follow the Code of Conduct below

---

## 📝 Code of Conduct

- **Be Respectful**: Treat all contributors with respect
- **Be Inclusive**: Welcome people of all backgrounds and experience levels
- **Be Constructive**: Provide helpful feedback and criticism
- **Be Honest**: Give credit where it's due
- **Report Issues**: Report harassment/inappropriate behavior to maintainers

---

## 🔄 Contribution Types

### 1. Bug Reports 🐛

**Report bugs by creating GitHub Issues**

Include:
- Clear description of the bug
- Steps to reproduce
- Expected behavior
- Actual behavior
- Screenshots if applicable
- Environment (OS, browser, Node version)

Example:
```
### Bug: Temples page not loading

**Description**: The temples page shows a blank screen

**Steps to Reproduce**:
1. Navigate to /temples
2. Wait 5 seconds

**Expected**: Temples list should load
**Actual**: Blank screen with no error

**Environment**: Windows 10, Chrome 120, Node 18.0.0
```

### 2. Feature Requests ✨

**Suggest features via GitHub Discussions or Issues**

Include:
- Clear feature description
- Why it's needed
- How it would work
- Potential user impact

Example:
```
### Feature: Email notifications for temple events

**Description**: Users should receive email notifications when new festival events are added to temples they follow

**Use Case**: Pilgrims want to know about upcoming festivals in advance
```

### 3. Documentation Improvements 📚

**Update or improve documentation**

- Fix typos and grammar
- Clarify confusing sections
- Add examples
- Update outdated information

### 4. Code Contributions 💻

**Submit code fixes and features**

See "Development Workflow" below.

---

## 🛠️ Development Workflow

### Step 1: Fork the Repository

```bash
# Fork on GitHub, then clone your fork
git clone https://github.com/YOUR_USERNAME/DarshanEase.git
cd DarshanEase
```

### Step 2: Create a Feature Branch

```bash
# Create branch from main/development
git checkout -b feature/your-feature-name
# or for bug fixes
git checkout -b fix/bug-description
```

**Branch Naming**:
- `feature/feature-name` - New features
- `fix/bug-description` - Bug fixes
- `docs/doc-update` - Documentation
- `refactor/component-name` - Code refactoring
- `perf/optimization-name` - Performance improvements

### Step 3: Set Up Development Environment

```bash
# Install dependencies
npm run install-all

# Copy env files
cp backend/.env.example backend/.env
cp frontend/.env.local.example frontend/.env.local

# Start development servers
npm start
```

### Step 4: Make Changes

- Make focused changes related to your feature/fix
- Follow coding standards (see below)
- Add tests for new features
- Update documentation as needed

### Step 5: Test Changes

```bash
# Frontend tests
cd frontend && npm test

# Backend tests
cd backend && npm test

# Lint frontend
cd frontend && npm run lint

# Manual testing
npm start  # Test in browser
```

### Step 6: Commit Changes

```bash
# Stage changes
git add .

# Commit with descriptive message
git commit -m "feat: add temple search functionality"
```

**Commit Message Format**:
```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting, missing semicolons, etc.
- `refactor`: Code restructuring
- `perf`: Performance improvements
- `test`: Adding tests
- `chore`: Build process, dependencies

**Examples**:
```
feat(temples): add search by deity
fix(map): resolve marker clustering issue
docs: update API documentation
refactor(components): extract reusable component
perf(api): add response caching
```

### Step 7: Push to Your Fork

```bash
git push origin feature/your-feature-name
```

### Step 8: Create Pull Request

1. Go to GitHub
2. Click "Compare & pull request"
3. Fill in PR template:

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation
- [ ] Refactoring

## Related Issues
Fixes #123

## Testing
- [ ] Tested locally
- [ ] Added tests
- [ ] Updated documentation

## Screenshots (if applicable)
Add screenshots for UI changes
```

### Step 9: Code Review

- Respond to reviewer comments
- Make requested changes
- Push updates (will auto-update PR)
- Wait for approval before merging

---

## 📏 Coding Standards

### JavaScript/TypeScript

```typescript
// Use TypeScript for type safety
interface Temple {
  name: string;
  location: string;
  deity: string;
}

// Use arrow functions
const getTemple = (id: string): Promise<Temple> => {
  // ...
};

// Use const by default
const MAX_TEMPLES = 100;

// Destructuring
const { name, location } = temple;

// Template literals
const message = `Found ${temples.length} temples`;
```

### React Components

```tsx
// Functional components with TypeScript
interface TempleCardProps {
  temple: Temple;
  onSelect?: (temple: Temple) => void;
}

const TempleCard: React.FC<TempleCardProps> = ({ temple, onSelect }) => {
  return (
    <div className="temple-card">
      <h2>{temple.name}</h2>
      <p>{temple.location}</p>
    </div>
  );
};

export default TempleCard;
```

### Naming Conventions

- Variables/functions: `camelCase`
- Classes/components: `PascalCase`
- Constants: `UPPER_SNAKE_CASE`
- Private properties: `_camelCase`

### Comments

```typescript
// Good: Explain why, not what
// Cache temples for 1 hour to reduce API calls
const getCachedTemples = () => {
  // ...
};

// Avoid: States the obvious
// Get all temples
const getAllTemples = () => {
  // ...
};

// Use JSDoc for public APIs
/**
 * Fetches temples by location
 * @param location - City or region name
 * @returns Array of temples in that location
 */
const getTemplesByLocation = (location: string): Temple[] => {
  // ...
};
```

### File Organization

```
src/
├── components/
│   ├── TempleCard.tsx
│   ├── TempleList.tsx
│   └── index.ts
├── pages/
│   ├── Temples.tsx
│   └── TempleDetails.tsx
├── services/
│   └── apiService.ts
├── types/
│   └── index.ts
├── utils/
│   └── helpers.ts
└── App.tsx
```

### Frontend Code Structure

```tsx
import React from 'react';
import { useEffect, useState } from 'react';
import styles from './Component.module.css';
import { TempleAPI } from '@/services/apiService';

// Types
interface ComponentProps {
  id: string;
}

// Component
const MyComponent: React.FC<ComponentProps> = ({ id }) => {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    // Effect logic
  }, [id]);

  return (
    <div className={styles.container}>
      {/* JSX */}
    </div>
  );
};

export default MyComponent;
```

### Backend Code Structure

```javascript
// models/Temple.js
const templeSchema = new Schema({
  name: { type: String, required: true },
  location: { type: String, required: true },
  // ...
});

module.exports = mongoose.model('Temple', templeSchema);

// routes/templeRoutes.js
router.get('/', async (req, res) => {
  try {
    const temples = await Temple.find();
    res.json({ success: true, data: temples });
  } catch (error) {
    res.status(500).json({ success: false, error: error.message });
  }
});
```

---

## 🧪 Testing Guide

### Frontend Testing

```bash
# Run tests
npm test

# Run with coverage
npm test -- --coverage

# Run specific test
npm test -- TempleCard.test.tsx
```

**Test Example**:
```typescript
import { render, screen } from '@testing-library/react';
import TempleCard from './TempleCard';

describe('TempleCard', () => {
  it('renders temple name', () => {
    const temple = { name: 'Krishna Temple', location: 'Mathura' };
    render(<TempleCard temple={temple} />);
    expect(screen.getByText('Krishna Temple')).toBeInTheDocument();
  });
});
```

### Backend Testing

```bash
# Run tests
npm test

# Run specific test
npm test -- temples.test.js

# Run with coverage
npm test -- --coverage
```

---

## 📮 Pull Request Process

1. **Before Submitting**
   - [ ] Tests pass
   - [ ] Linter passes
   - [ ] Code follows style guide
   - [ ] Documentation updated
   - [ ] No merge conflicts

2. **PR Description**
   - Clear title: `feat: add temple search`
   - Describe changes
   - Link related issues
   - Include screenshots for UI changes
   - Note breaking changes

3. **Review Process**
   - Assigned to reviewer
   - Feedback provided
   - Make changes if requested
   - Approved and merged

4. **After Merge**
   - Delete branch
   - Thank you for contribution!

---

## 🐛 Bug Fix Process

1. Create issue describing bug
2. Create branch from issue
3. Fix bug with tests
4. Submit PR with:
   - Link to issue
   - Steps to verify fix
   - Test coverage

---

## ✨ Feature Development Process

1. Create feature request issue
2. Discuss implementation approach
3. Create feature branch
4. Implement feature
5. Add tests
6. Update documentation
7. Submit PR

---

## 📚 Resources

- **React Documentation**: [react.dev](https://react.dev/)
- **TypeScript Documentation**: [typescriptlang.org](https://www.typescriptlang.org/)
- **Express.js Documentation**: [expressjs.com](https://expressjs.com/)
- **MongoDB Documentation**: [docs.mongodb.com](https://docs.mongodb.com/)
- **Git Guide**: [git-scm.com/book](https://git-scm.com/book/en/v2)

---

## 🆘 Getting Help

- **Questions**: Open GitHub Discussion
- **Stuck**: Post in GitHub Issues with context
- **Chat**: Join community discussions
- **Email**: sachinsoniofficial2003@gmail.com

---

## 🎉 Recognition

Contributors will be:
- Added to CONTRIBUTORS.md
- Listed in Release Notes
- Recognized in community discussions
- Thanked in commit messages

---

## 📋 Contribution Checklist

Before submitting PR:

- [ ] Fork and cloned repository
- [ ] Created feature branch with descriptive name
- [ ] Made focused changes
- [ ] Followed coding standards
- [ ] Added/updated tests
- [ ] Updated documentation
- [ ] Committed with descriptive messages
- [ ] Pushed to fork
- [ ] Created PR with detailed description
- [ ] Linked related issues
- [ ] Requested review

---

## ❓ FAQ

**Q: Can I contribute without coding experience?**
A: Yes! Documentation, design, testing, and bug reporting all help.

**Q: How long do PRs take to review?**
A: Usually 2-7 days depending on complexity.

**Q: Can I work on something that's already an issue?**
A: Comment on the issue first to coordinate effort.

**Q: What if my PR is rejected?**
A: It happens! Get feedback and you can always improve and resubmit.

**Q: How do I become a maintainer?**
A: Contribute consistently, gain trust, then ask in discussions.

---

## 🙏 Thank You!

Your contributions make DARSHAN EASE better for everyone. We truly appreciate your help in making temple discovery easier for devotees worldwide!

---

**Version**: 1.0.0  
**Last Updated**: February 25, 2026  
**Status**: ✅ Complete Contribution Guide
