tried prisma for the first time and took a deep look on migrations, conclusion is prisma is so powerful
made these notes too, but unfortunatley the images won't show here:
- **Making a new database
	- `When you define your schema in Prisma's `schema.prisma` file, Prisma migrations take care of generating the raw SQL required to apply those schema changes to your database. Here’s how the process works:`
	
	1. **Define Schema in Prisma**: You write your data model in the `schema.prisma` file using Prisma’s schema language. This includes defining tables (models), columns, relationships, and constraints.
	
	3. **Generate Migration Files**: When you run a migration command (like `npx prisma migrate dev --name init`), Prisma reads your schema file and generates SQL migration files. These SQL files contain all the commands necessary to create or modify the database structure to match your Prisma schema.
		- omitting the `--name` flag would make the command ask you to enter the migration name manually
		
	4. **Apply Migrations**: Prisma then applies the generated SQL migration files to the actual database, so your database schema aligns with your Prisma schema definition.
		- `npx prisma migrate --create-only` will only create the migration files but not run it
		- after the migrations are created you can modify the SQL 
			- one example is renaming an existing column would drop the original one with it's data when doing migrating:![[Pasted image 20241106153552.png]]
			- so you use `--create-only` flag to only create the migration, then modify it manually: ![[Pasted image 20241106153909.png]]
		
	5. **Keep Track of Changes**: Each migration is stored in a `prisma/migrations` folder, with a unique timestamped folder for each migration. This folder contains the SQL commands and helps Prisma track which migrations have been applied to which database.
- **Pulling Existing DB
	- **Define DB source in schema.prisma file:** ![[Pasted image 20241106155831.png]]
	- **`npx prisma db pull` command will copy the original DB tables, you can then modify it and use migrations to apply these modifications**
