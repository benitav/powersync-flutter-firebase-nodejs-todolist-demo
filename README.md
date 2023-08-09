# PowerSync + Supabase Flutter Demo: Todo List App

Demo app demonstrating use of the PowerSync SDK for Flutter together with Supabase.

# Running the app

Install the Flutter SDK, then:

```sh
flutter pub get
flutter run
```

# Setup Supabase Project

Create a new Supabase project, and paste an run the contents of [database.sql](./database.sql) in the Supabase SQL editor.

It does the following:

1. Create `lists` and `todos` tables.
2. Create a publication called `powersync` for `lists` and `todos`.
3. Enable row level security, allowing users to only view and edit their own data.
4. Create a trigger to populate some sample data when an user registers.


# Setup PowerSync Instance

Create a new PowerSync instance, connecting to the database of the Supabase project.

Then deploy the following sync rules:

```yaml
bucket_definitions:
  user_lists:
    # Separate bucket per todo list
    parameters: select id as list_id from lists where owner_id = token_parameters.user_id
    data:
      - select * from lists where id = bucket.list_id
      - select * from todos where list_id = bucket.list_id
```

# Configure the app

Edit [lib/app_config.dart](./lib/app_config.dart), using the credentials of your new
Supabase and PowerSync projects.

