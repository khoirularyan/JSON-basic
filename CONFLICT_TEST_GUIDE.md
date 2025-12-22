# 🔥 Panduan Testing Conflict Resolver

Repositori ini sudah disiapkan dengan skenario conflict yang siap untuk menguji aplikasi conflict resolver Anda.

## 📋 Daftar Branch

| Branch | File | Perubahan | Conflict Dengan |
|--------|------|-----------|-----------------|
| `main` | - | Baseline (original state) | - |
| `feature-a` | `companies.js` | name: "Bank Central Asia"<br>address: "Jakarta Pusat"<br>value: 5000 | `feature-b` |
| `feature-b` | `companies.js` | name: "BCA Bank"<br>address: "Sudirman Street 123"<br>value: 3000 | `feature-a` |
| `feature-c` | `index.html` | title: "Company Management System"<br>+ company: "Tech Solutions" | `feature-d` |
| `feature-d` | `index.html` | title: "Corporate Data Portal"<br>+ company: "Global Finance Corp" | `feature-c` |

---

## 🧪 Skenario Testing

### **Skenario 1: Conflict di `companies.js`**

Kedua branch mengubah baris yang sama dengan nilai berbeda.

#### Langkah Testing:

```bash
# 1. Checkout ke main
git checkout main

# 2. Merge feature-a (akan sukses)
git merge feature-a

# 3. Merge feature-b (akan CONFLICT!)
git merge feature-b
```

#### Expected Conflict:

```javascript
<<<<<<< HEAD
    name: "Bank Central Asia",
    address: "Jakarta Pusat",
    value: 5000,
=======
    name: "BCA Bank",
    address: "Sudirman Street 123",
    value: 3000,
>>>>>>> feature-b
```

#### Reset untuk test ulang:
```bash
git merge --abort
git reset --hard origin/main
```

---

### **Skenario 2: Conflict di `index.html`**

Kedua branch mengubah title dan menambahkan company berbeda.

#### Langkah Testing:

```bash
# 1. Checkout ke main
git checkout main

# 2. Merge feature-c (akan sukses)
git merge feature-c

# 3. Merge feature-d (akan CONFLICT!)
git merge feature-d
```

#### Expected Conflict:

**Conflict 1 - Title:**
```html
<<<<<<< HEAD
    <title>Company Management System</title>
=======
    <title>Corporate Data Portal</title>
>>>>>>> feature-d
```

**Conflict 2 - Company Array:**
```javascript
<<<<<<< HEAD
        {
          name: "Tech Solutions",
          address: "Innovation Park 100",
          value: 7500,
          employees: 150,
          products: ["software", "consulting", "cloud services"],
          isActive: true,
        },
=======
        {
          name: "Global Finance Corp",
          address: "Wall Street 500",
          value: 12000,
          employees: 300,
          products: ["trading", "investment", "wealth management"],
          isActive: true,
        },
>>>>>>> feature-d
```

#### Reset untuk test ulang:
```bash
git merge --abort
git reset --hard origin/main
```

---

## 🎯 Testing dengan Aplikasi Conflict Resolver

### Checklist Fitur yang Harus Ditest:

- [ ] **Deteksi Conflict**: Aplikasi harus bisa detect conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)
- [ ] **Tampilkan Kedua Versi**: Harus menampilkan versi HEAD dan versi incoming branch
- [ ] **Pilih Resolusi**: User bisa pilih:
  - Accept Current (HEAD)
  - Accept Incoming (branch yang di-merge)
  - Accept Both
  - Manual Edit
- [ ] **Preview**: Tampilkan preview hasil sebelum save
- [ ] **Save & Commit**: Setelah resolve, bisa save dan commit hasil

---

## 🔄 Skenario Testing Alternatif

### Test dengan Pull Request di GitHub:

1. **Buat PR**: `feature-a` → `main`
2. **Merge PR** (akan sukses)
3. **Buat PR**: `feature-b` → `main`
4. **Lihat Conflict** di GitHub UI
5. **Test Resolver** untuk resolve conflict

### Test dengan Rebase:

```bash
# Checkout feature-b
git checkout feature-b

# Rebase ke main (yang sudah ada feature-a)
git rebase main
# Akan CONFLICT!

# Test aplikasi resolver untuk resolve
```

---

## 📊 Statistik Conflict

| Skenario | File | Jumlah Conflict | Baris yang Conflict |
|----------|------|-----------------|---------------------|
| feature-a vs feature-b | companies.js | 1 conflict | 3 lines (name, address, value) |
| feature-c vs feature-d | index.html | 2 conflicts | Title (1 line) + Company array (8 lines) |

---

## 💡 Tips Testing

1. **Selalu reset ke clean state** sebelum test ulang:
   ```bash
   git merge --abort
   git reset --hard origin/main
   ```

2. **Gunakan `git status`** untuk cek file yang conflict:
   ```bash
   git status
   ```

3. **Lihat conflict markers** dengan text editor atau `git diff`:
   ```bash
   git diff
   ```

4. **Test berbagai resolusi**:
   - Accept current
   - Accept incoming
   - Accept both (gabungkan keduanya)
   - Custom edit

---

## ✅ Verifikasi Hasil

Setelah resolve conflict, pastikan:

1. **No conflict markers** tersisa di file
2. **File valid** (syntax benar)
3. **Git status clean** setelah commit:
   ```bash
   git add .
   git commit -m "Resolved conflict"
   git status
   ```

---

## 🚀 Quick Start

```bash
# Clone repo
git clone https://github.com/khoirularyan/JSON-basic.git
cd JSON-basic

# Test Skenario 1
git checkout main
git merge feature-a
git merge feature-b  # CONFLICT!

# Gunakan aplikasi conflict resolver Anda di sini

# Reset
git merge --abort
git reset --hard origin/main

# Test Skenario 2
git merge feature-c
git merge feature-d  # CONFLICT!

# Gunakan aplikasi conflict resolver Anda di sini
```

---

**Happy Testing! 🎉**
