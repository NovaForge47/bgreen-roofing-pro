## Το sitemap είναι πλέον ONLINE και σωστό

Έλεγξα το `https://bgreen.gr/sitemap.xml` αυτή τη στιγμή:

- **HTTP 200 OK** (όχι πια 404)
- **Content-Type: application/xml**
- Επιστρέφει έγκυρο XML με το `https://bgreen.gr/` μέσα

Το μήνυμα που βλέπεις στο Google Search Console («HTTP Error: 404») είναι από **παλιότερη προσπάθεια** της Google να διαβάσει το sitemap πριν δημοσιευτεί το fix. Το GSC δεν ξαναδοκιμάζει αυτόματα αμέσως — χρειάζεται να του πεις εσύ να ξαναδιαβάσει.

## Τι να κάνεις στο Google Search Console (χωρίς αλλαγές στον κώδικα)

1. Άνοιξε **Sitemaps** στο GSC.
2. Στη λίστα με τα υποβεβλημένα sitemaps, δίπλα στο `sitemap.xml` πάτα το μενού (⋮) και κάνε **Remove sitemap**.
3. Πάτα **Add a new sitemap**, γράψε `sitemap.xml` και **Submit**.
4. Μετά από 1–2 λεπτά το status θα γίνει **Success** και θα δεις 1 discovered URL.
5. Πήγαινε στο **URL Inspection**, βάλε `https://bgreen.gr/`, πάτα **Test live URL** και μετά **Request indexing**.

## Καμία αλλαγή στον κώδικα δεν χρειάζεται

Το sitemap route, το `robots.txt`, το canonical, και το JSON-LD δουλεύουν σωστά στο live site. Αν μετά το re-submit εξακολουθεί να δείχνει 404, ενημέρωσέ με να ελέγξω ξανά.
