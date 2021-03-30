# MassSpecBlocks
MassSpecBlocks: Database of Sequences and Building Blocks of Microbial Metabolites for Mass Spectra Analysis is an open-source web application to manage own user databases of chemical structures like NRPs and to find structures on other chemical projects like [Pubchem](https://pubchem.ncbi.nlm.nih.gov), [ChemSpider](http://www.chemspider.com), [Norine](https://bioinfo.lifl.fr/norine/) and [ChEBI](https://www.ebi.ac.uk/chebi/downloadsForward.do). The application provides an export format for open source program [Cyclobranch](https://ms.biomed.cas.cz/cyclobranch/docs/html/) from Jiří Novák (Laboratory of Molecular Structure Characterization - Academy of Sciences of the Czech Republic).

# Quick Links

[Frontend repo](https://github.com/privrja/thesis-frontend-react)

[Backend repo](https://github.com/privrja/thesis)

[SmilesDrawer](https://github.com/privrja/smilesDrawer)

# Application Info
Application has separated frontend and backend. **Frontend** is developed in React with typescript and has its own [frontend repo](https://github.com/privrja/thesis-frontend-react). **Backend** is written in PHP with Symfony framework, [backend repo](https://github.com/privrja/thesis). Application is developed for Mysql 8 /MariaDB 10, but when using Symfony you can create your migrations for another database. The application uses many other libraries like [SmilesDrawer](https://github.com/privrja/smilesDrawer) from **Daniel Probst** to draw chemical structures from SMILES format or [JSME](https://jsme-editor.github.io) from **Peter Ertl and Bruno Bienfait** to editing chemical structures. Application is based on previous application [Bbdgnc](https://github.com/privrja/bbdgnc). The application was developed within the diploma thesis MassSpecBlocks: **MassSpecBlocks: Database of Sequences and Building Blocks of Microbial Metabolites for Mass Spectra Analysis**, Jan Přívratský, FIT CTU Prague, 2021. Supervisor **Jiří Novák**

# Documentation
TODO all documentation and detailed descriptions should be in this repo.

Documentation of the databse structures is in [DataModelDescription.md](https://github.com/privrja/MassSpecBlocks/blob/main/DataModelDescription.md).
