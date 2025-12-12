# Cahier de Charges – Package “Moroccan Dev Utilities”

## 1️⃣ Nom du projet
**moroccan-utils**  

---

## 2️⃣ Description du projet
Package JavaScript/TypeScript pour développeurs web et applications au Maroc, résolvant des problèmes fréquents lors de la manipulation de :  
1. **Données des administrations et institutions marocaines**  
2. **Numéros d'identité nationale / CIN**  
3. **Adresses marocaines (villes et quartiers)**  
4. **Valeurs monétaires locales (MAD)**  
5. **Intégration avec services marocains populaires**  

---

## 3️⃣ Modules principaux

### 3.1 Data Cleaning Module
- **normalizeName(name: string, lang?: "ar" | "fr" | "en"): string**  
  - Normalise les noms en arabe, français et anglais.  
- **parseDate(dateStr: string, format?: string): Date**  
  - Convertit différentes formats de dates (Hijri, Grégorien, CSV, Excel) en date JS unifiée.  
- **convertCSVToJSON(csvString: string): object[]**  
  - Convertit un CSV en tableau JSON prêt à l’emploi.  
- **cleanExcelData(filePath: string): object[]**  
  - Convertit et nettoie des données Excel pour la base de données.

---

### 3.2 CIN Module
- **validateCIN(cin: string): boolean**  
  - Vérifie la validité d’un numéro CIN.  
- **parseCIN(cin: string): object**  
  - Extrait les informations du citoyen depuis le CIN : date de naissance, sexe, code ville.  
- **generateCIN(options?: object): string**  
  - Génère des CIN fictifs valides pour tests.

---

### 3.3 Address Module
- **normalizeCity(name: string, lang?: string): string**  
  - Unifie le nom de la ville en arabe/français/anglais.  
- **normalizeDistrict(city: string, district: string, lang?: string): string**  
  - Unifie le nom du quartier selon la ville.  
- **listCities(lang?: string): string[]**  
  - Liste des villes marocaines supportées.  
- **listDistricts(city: string, lang?: string): string[]**  
  - Liste des quartiers pour chaque ville.

---

### 3.4 Currency Module
- **formatMAD(amount: number): string**  
  - Formate un montant en dirhams marocains avec les séparateurs décimaux.  
- **convertToCents(amount: number): number**  
  - Convertit un montant MAD en centimes.

---

### 3.5 Moroccan Services Integration Module
- **baridBankAPI(endpoint: string, options: object): Promise<any>**  
- **cihAPI(endpoint: string, options: object): Promise<any>**  
- **marocTelecommerceAPI(endpoint: string, options: object): Promise<any>**  
- **marocCloudAPI(endpoint: string, options: object): Promise<any>**  
  - Interfaces simples pour intégrer les services marocains populaires avec gestion de l’authentification et des erreurs.

---

## 4️⃣ Exemples d’utilisation (React / JS)

```javascript
// Avant Moroccan Utils
function checkCIN(cin) {
    // Code from scratch to check CIN
}
function getCityName(name) {
    // Each time re-write same logic
}

// Après Moroccan Utils
import { validateCIN, parseCIN, normalizeCity, formatMAD } from 'moroccan-utils';

const cin = "AB123456";
console.log(validateCIN(cin)); // true
console.log(parseCIN(cin)); // { dob: "1990-05-12", gender: "M", cityCode: "12" }

console.log(normalizeCity("Casa")); // "الدار البيضاء"
console.log(formatMAD(12345.67)); // "12,345.67 MAD"
