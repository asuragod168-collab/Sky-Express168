# Sky Express — Website គ្រប់គ្រងការដឹកជញ្ជូន

Website Responsive សម្រាប់ Android, iPhone/iOS និង PC។ បង្កើតដោយ React + Vite និង Supabase (Authentication + PostgreSQL Database)។

## អ្វីដែលមានក្នុងគម្រោងនេះ

- Dashboard និងស្ថិតិបញ្ញើ
- បង្កើតបញ្ញើថ្មី និងលេខ Tracking
- ស្វែងរកតាមលេខកូដ អ្នកទទួល លេខទូរស័ព្ទ និងអាសយដ្ឋាន
- កែស្ថានភាព៖ រង់ចាំទទួល / បានទទួលបញ្ញើ / កំពុងដឹក / បានដឹកជញ្ជូន / បានលុបចោល
- សង្ខេប COD និងថ្លៃដឹក
- Login តាម Supabase Auth
- ផ្ទាំង Admin មើលបញ្ជីអ្នកប្រើ និងកំណត់តួនាទី Admin/Staff
- Demo Mode មានទិន្នន័យគំរូ (ទិន្នន័យ Demo មិនត្រូវបានរក្សាទុកក្រោយ refresh)
- Responsive design សម្រាប់ទូរស័ព្ទ និងកុំព្យូទ័រ

> ចំណាំ៖ នេះជាគម្រោងចាប់ផ្តើមដែលអាចដាក់ Online បាន ប៉ុន្តែមុនប្រើក្នុងអាជីវកម្មពិត ត្រូវបង្កើត Supabase project, បង្កើត Admin users, ពិនិត្យ Row Level Security, backup និងសាកល្បងលំហូរការងារទាំងអស់។ មិនទាន់មាន GPS live tracking, SMS/Telegram notification, បោះពុម្ពស្លាក, ឬ role-based permissions ពេញលេញទេ។

## 1. ត្រូវមានអ្វីខ្លះ

- កុំព្យូទ័រ Windows/Mac សម្រាប់ដំឡើង និងដាក់ Online ងាយស្រួលជាងទូរស័ព្ទ
- Node.js LTS: https://nodejs.org/
- គណនី Supabase: https://supabase.com/
- គណនី GitHub: https://github.com/ (ជាជម្រើស ប៉ុន្តែងាយសម្រាប់ deploy)
- គណនី Vercel: https://vercel.com/ ឬ Netlify

## 2. បង្កើត Database និង Login

1. ចូល Supabase ហើយបង្កើត Project ថ្មីឈ្មោះ `sky-express`។
2. រក្សា Database password ឱ្យមានសុវត្ថិភាព។
3. ចូល `SQL Editor` → `New query`។
4. បើកឯកសារ `supabase/schema.sql` ក្នុងគម្រោងនេះ ចម្លងកូដទាំងអស់ទៅ SQL Editor ហើយចុច `Run`។
5. ចូល `Project Settings` → `API` (ឬ Connect) រក `Project URL` និង `Publishable key`/`anon key`។
6. ចូល `Authentication` → `Users` → `Add user` ដើម្បីបង្កើតគណនីដំបូង។ ប្រើអ៊ីមែល និងពាក្យសម្ងាត់ខ្លាំង។ កុំបើក public sign-up ប្រសិនបើ website សម្រាប់បុគ្គលិកតែប៉ុណ្ណោះ។
7. បន្ទាប់ពីបង្កើតអ្នកប្រើដំបូង សូមចូល `SQL Editor` ហើយដំណើរការពាក្យបញ្ជា SQL ខាងក្រោម ដោយប្តូរ `EMAIL` ជាអ៊ីមែលពិតរបស់អ្នកគ្រប់គ្រង៖

```sql
update public.profiles
set role = 'admin'
where id = (select id from auth.users where email = 'EMAIL');
```

8. បុគ្គលិកដែលបង្កើតបន្ទាប់ នឹងទទួលតួនាទី `staff` ដោយស្វ័យប្រវត្តិ។ Admin អាចចូលផ្ទាំង `អ្នកប្រើប្រាស់` ដើម្បីប្តូរតួនាទីរបស់អ្នកដទៃ។ គណនីដែលកំពុង Login មិនអាចប្តូរតួនាទីខ្លួនឯងពី UI បានទេ។
9. សូមពិនិត្យ RLS policies មុនដាក់ប្រើទិន្នន័យអតិថិជនពិត។

## 3. ដំណើរការលើកុំព្យូទ័រ

Unzip project នេះ រួចបើក Terminal/Command Prompt នៅក្នុង folder `sky-express` ហើយដំណើរការ៖

```bash
npm install
```

ចម្លង `.env.example` ទៅជា `.env` ហើយបំពេញព័ត៌មាន Supabase៖

```env
VITE_SUPABASE_URL=https://YOUR_PROJECT_ID.supabase.co
VITE_SUPABASE_ANON_KEY=YOUR_SUPABASE_PUBLISHABLE_OR_ANON_KEY
```

ប្រើតែ Publishable/anon key នៅ frontend ប៉ុណ្ណោះ។ **កុំដាក់ `service_role` key នៅក្នុង website ឬ GitHub ជាដាច់ខាត។**

បន្ទាប់មក៖

```bash
npm run dev
```

បើក URL ដែល Terminal បង្ហាញ (ជាទូទៅ `http://localhost:5173`)។

## 4. ដាក់ Online ដោយ Vercel

1. បង្កើត repository ថ្មីនៅ GitHub ហើយ upload project នេះទៅ repository។
2. ចូល https://vercel.com/ → Add New → Project → Import Git Repository។
3. ជ្រើស repository `sky-express`។
4. Framework ជ្រើស Vite (ឬ Vercel ស្គាល់ដោយស្វ័យប្រវត្តិ)។
5. នៅ Environment Variables បន្ថែម៖
   - `VITE_SUPABASE_URL` = Project URL របស់ Supabase
   - `VITE_SUPABASE_ANON_KEY` = Publishable/anon key របស់ Supabase
6. ចុច Deploy។
7. បន្ទាប់ពី Deploy រួច Vercel នឹងផ្តល់ URL ដូចជា `https://your-project.vercel.app`។ អ្នកអាចបើក URL នេះពី Android, iPhone និង PC។
8. រាល់ពេលកែ Source Code ហើយ push ទៅ GitHub វានឹង Deploy ថ្មីដោយស្វ័យប្រវត្តិ (ប្រសិនបើបានភ្ជាប់ Git)។

## 5. ការប្រើប្រាស់

1. បើក Website ហើយ Login ដោយអ្នកប្រើដែលបង្កើតក្នុង Supabase។
2. ចុច `បង្កើតបញ្ញើថ្មី` ហើយបំពេញអ្នកទទួល អាសយដ្ឋាន និងព័ត៌មាន COD។
3. ប្រើ `បញ្ញើទាំងអស់` ដើម្បីស្វែងរក ឬកែស្ថានភាព។
4. Dashboard និងហិរញ្ញវត្ថុគណនាពីទិន្នន័យក្នុង Database។

## 6. សុវត្ថិភាពមុនប្រើជាមួយអតិថិជនពិត

- កុំប្រើទិន្នន័យគំរូជាទិន្នន័យអតិថិជនពិត។
- កុំចែករំលែក Supabase service role key ឬ Database password។
- សាកល្បង RLS និងតួនាទី Admin/Staff ជាមួយគណនីច្រើន មុនអនុញ្ញាតបុគ្គលិកច្រើនប្រើ។
- បង្កើតគោលការណ៍ backup និងអ្នកទទួលខុសត្រូវលើទិន្នន័យ។
- សាកល្បងការបង្កើតបញ្ញើ កែស្ថានភាព និងគណនា COD មុនប្រើជាផ្លូវការ។
- សូមកត់សម្គាល់ថា `created_by` អាច null សម្រាប់ការធ្វើតេស្ត ប៉ុន្តែគួរបង្ខំឱ្យមានអ្នកបង្កើតនៅ production។
