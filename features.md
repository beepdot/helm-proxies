# helm-demo

### Features in Demo:
- Charts availability as a helm repo
- Usage of dependent modules as subcharts
- Common template code for general or useful functions
- Each chart represented as a standalone chart
- Sharing variables between parent and child OR global values across charts
- Schema files for validation of data types
- Hooks for migrations, updates etc,.
- Post install notes and Post install validation messages
- Each component as a standalone helm chart and an independent release
- Auto Secrets injection into requires charts
- General idea on how to test a chart post install
- Favoring helm functions / new services rather than ansible
- Almost everything has a default value
- Upgrading few services
- Private repo overrides
- Fail on missing vars, fail on incompatible kubernetes version

### Future Features:
- Some sort of wrapper to run all the charts on new install and wrappers for each upgrade
- Github actions to auto update chart versions on helm repo on each commit / tag
- Chart testing using circle ci or helm github actions on full installtion along with functional test cases
- Operators for backup and restore and other operations
- Monitoring metrics and log parsing enabling / disabling with a flag
- End of install helm chart to get all values and store in a file to be stored in private repo
