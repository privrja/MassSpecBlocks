# MassSpecBlocks
MassSpecBlocks: Database of Sequences and Building Blocks of Microbial Metabolites for Mass Spectra Analysis is an open-source web application to manage own user databases of chemical structures like NRPs and to find structures on other chemical projects like [Pubchem](https://pubchem.ncbi.nlm.nih.gov), [ChemSpider](http://www.chemspider.com), [Norine](https://bioinfo.lifl.fr/norine/), [ChEBI](https://www.ebi.ac.uk/chebi/downloadsForward.do), [COCONUT](https://coconut.naturalproducts.net) and [NP Atlas](https://www.npatlas.org). The application provides an export format for open source program [CycloBranch](https://ms.biomed.cas.cz/cyclobranch/docs/html/) from Jiří Novák (Laboratory of Molecular Structure Characterization - Academy of Sciences of the Czech Republic).

# Quick Links

[Frontend repo](https://github.com/privrja/thesis-frontend-react)

[Backend repo](https://github.com/privrja/thesis)

[SmilesDrawer](https://github.com/privrja/smilesDrawer)

# Application Info
Application has separated frontend and backend. **Frontend** is developed in React with typescript and has its own [frontend repo](https://github.com/privrja/thesis-frontend-react). **Backend** is written in PHP with Symfony framework, [backend repo](https://github.com/privrja/thesis). Application is developed for Mysql 8 /MariaDB 10, but when using Symfony you can create your migrations for another database. The application uses many other libraries like [SmilesDrawer](https://github.com/privrja/smilesDrawer) from **Daniel Probst** to draw chemical structures from SMILES format or [JSME](https://jsme-editor.github.io) from **Peter Ertl and Bruno Bienfait** to editing chemical structures. Application is based on previous application [Bbdgnc](https://github.com/privrja/bbdgnc). The application was developed within the diploma thesis MassSpecBlocks: **MassSpecBlocks: Database of Sequences and Building Blocks of Microbial Metabolites for Mass Spectra Analysis**, Jan Přívratský, FIT CTU Prague, 2021. Supervisor **Jiří Novák**
If you want to cite us, please use a [10.1186/s13321-021-00530-2](https://jcheminf.biomedcentral.com/articles/10.1186/s13321-021-00530-2).

# Documentation

Application [Tutorial.md](https://github.com/privrja/MassSpecBlocks/blob/main/Tutorial.md) or a video [Tutorial](https://www.youtube.com/watch?v=5y8_Ou8luh0) on Youtube.

Documentation of the database structures is in [DataModelDescription.md](https://github.com/privrja/MassSpecBlocks/blob/main/DataModelDescription.md).

How to run application localy for development is described in [Local.md](https://github.com/privrja/MassSpecBlocks/blob/main/Local.md).

Documentation of the deployment to server is in [Deploy.md](https://github.com/privrja/MassSpecBlocks/blob/main/Deploy.md). 

When you approach to /rest/doc on backend there is a documentation page for REST API.

There is a tutorial to obtain [ChemSpider API key](https://github.com/privrja/MassSpecBlocks/blob/main/ChemSpiderKey.md).

# Versions

Latest version is **Alpa** [1.0.2 Alpa backend](https://github.com/privrja/thesis/releases/tag/1.0.2) and [1.0.2 Alpa frontend](https://github.com/privrja/thesis-frontend-react/releases/tag/1.0.2), compatibile with SmilesDrawer [2.1.6 Evenstar](https://github.com/privrja/smilesDrawer/releases/tag/2.1.6)

More info about version compatibility you can find in file [Version.md](https://github.com/privrja/MassSpecBlocks/blob/main/Version.md)



