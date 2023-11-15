# BlazorServerSQLite
/*Steps for setting up ASP.NET Blazor Server app for SQLite*/

1. Create a new project Blazor Server App as the type of application. This has been followed with individual accounts settings for Authentication.
2. Create a new class ApplicationUser under Data folder:
﻿using Microsoft.AspNetCore.Identity;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace REPLACEWITHNAMEOFPROJECT.Data
{
    public class ApplicationUser : IdentityUser
    {
    }
}

3. In ApplicationDbContext, change line public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
4. In ApplicationDbContext, add following code: 
     	protected override void OnModelCreating(ModelBuilder builder)
        {
            base.OnModelCreating(builder);
        }
5. In Programs.cs, change IdentityUser to ApplicationUser in AddDefaultIdentity.
6. In Areas/Identity/Pages/Shared/_LoginPartial and Areas/Identity/Pages/Account/LogOut, change from IdentityUser to ApplicationUser (needs reference to Data folder).
8. Install NuGet for SQLite (Manage NuGet Packages).
9. In Program.cs, replace UsqSqlServer with UseSqlite.
10. Replace value in ConnectionsStrings.DefaultConnection with "Data Source = REPLACEWITHDATABASENAME.db".
11. Remove existing migrations (Remove-Migration in Package Manager Consolethis) This step avoids getting the error sqlite error 1 'near max syntax error' - due to nvarchar(max) included for existing migrations for SQLServer database).
12. Add a migration called Initial (Add-Migration REPLACEWITHMIGRATIONNAME in Package Manager Console).
13. Update the database (Update-Database in Package Manager Console).
14. Test user registration.
