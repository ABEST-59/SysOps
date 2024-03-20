#Configuration LDAP

    - Parametres et Paramètres LDAP
    URI du serveur LDAP:
        ldap://PMDC1.ad-cimut.priv:389
    ND de la liaison LDAP
        CN=LDAP SYSOPS,OU=LDAP,OU=Admins Serveurs et Services,OU=Comptes techniques,OU=CIMUT,DC=ad-cimut,DC=priv
    Mot de passe de la liaison LDAP
        Mot de LDAP SYSOPS
    Type de groupe LDAP
        ActiveDirectoryGroupType
    Groupe LDAP obligatoire
        CN=GG_AWX_USERS,OU=Groupes Applications,OU=Groupes de sécurité,OU=CIMUT,DC=ad-cimut,DC=priv

    Recherche d'utilisateurs LDAP
    [
        [
        "OU=Comptes techniques,OU=CIMUT,DC=ad-cimut,DC=priv",
        "SCOPE_SUBTREE",
        "(sAMAccountName=%(user)s)"
        ],
        [
        "OU=Utilisateurs,OU=CIMUT,DC=ad-cimut,DC=priv",
        "SCOPE_SUBTREE",
        "(sAMAccountName=%(user)s)"
        ]
    ]

    Recherche de groupes LDAP
    [
        "OU=Groupes Applications,OU=Groupes de sécurité,OU=CIMUT,DC=ad-cimut,DC=priv",
        "SCOPE_SUBTREE",
        "(objectClass=group)"
    ]

    Mappe des attributs d'utilisateurs LDAP
    {
        "email": "mail",
        "first_name": "givenName",
        "last_name": "sn"
    }

    Paramètres de types de groupes LDAP
    {
        "name_attr": "cn"
    }

    Marqueurs d'utilisateur LDAP par groupe
    {
        "CIMUT_DSI": {
        "admins": "CN=GG_AWX_ADMIN,OU=Groupes Applications,OU=Groupes de sécurité,OU=CIMUT,DC=ad-cimut,DC=priv",
        "remove_admins": true,
        "remove_users": true,
        "users": true
        }
    }

    Mappe d'équipes LDAP
    {
        "IT Sys": {
        "organization": "CIMUT_DSI",
        "remove": true,
        "users": "CN=GG_AWX_ADMIN,OU=Groupes Applications,OU=Groupes de sécurité,OU=CIMUT,DC=ad-cimut,DC=priv"
        }
    }