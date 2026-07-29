Το Google Search Console δείχνει «Crawled - currently not indexed» και «Temporary processing error». Εντόπισα ένα πραγματικό τεχνικό πρόβλημα και ένα φυσιολογικό στάδιο για καινούρια site.

Τι βρήκα:

- **Sitemap URL mismatch**: Το `robots.txt` λέει `Sitemap: https://bgreen.gr/sitemap.xml`, αλλά το sitemap δημιουργείται στο `/sitemap/xml` (με slash). Το `https://bgreen.gr/sitemap.xml` επιστρέφει **404**. Αυτό εξηγεί το «Temporary processing error» στο GSC.
- **Canonical tag υπάρχει** στο live HTML (`<link rel="canonical" href="https://bgreen.gr/"/>`), οπότε το «User-declared canonical: N/A» είναι πιθανότατα από παλιότερο crawl ή από το HTTP redirect.
- **Stale deployment**: Το live site ακόμα δείχνει το παλιό hero text «Η Στέγη και το Σπίτι σας...» αντί για «Μεταλλικα Προκατ...». Οι τελευταίες αλλαγές δεν έχουν δημοσιευτεί.

Πλάνο δράσης:

1. **Διόρθωση sitemap route** — Μετονομασία/αλλαγή του `src/routes/sitemap.xml.ts` ώστε να σερβίρει στο σωστό URL `/sitemap.xml` (όχι `/sitemap/xml`). Ενημέρωση του `createFileRoute` αν χρειάζεται.
2. **Επαλήθευση robots.txt** — Επιβεβαίωση ότι δείχνει στο σωστό `https://bgreen.gr/sitemap.xml`.
3. **Re-publish** — Δημοσίευση του site για να ανέβουν οι διορθώσεις (canonical, sitemap, νέο hero text).
4. **Οδηγίες χρήστη για GSC** — Μετά τη δημοσίευση, να κάνει:
   - Delete + re-submit το sitemap στο Google Search Console.
   - Request indexing ξανά για το `https://bgreen.gr/`.
   - Υπομονή: «Crawled - currently not indexed» είναι φυσιολογικό για καινούρια site και μπορεί να πάρει από μερικές μέρες έως 2-4 εβδομάδες.

Τεχνικές λεπτομέρειες:

- Το route tree (`src/routeTree.gen.ts`) δείχνει `/sitemap/xml` αντί για `/sitemap.xml`. Θα φτιάξω το file-based routing για το dot.
- Θα τρέξω build πριν τη δημοσίευση για να επιβεβαιώσω ότι δεν υπάρχουν σφάλματα.
- Δεν απαιτείται αλλαγή στο canonical — ήδη υπάρχει σωστά.