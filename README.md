## ΑΡΧΙΤΕΚΤΟΝΙΚΗ ΠΡΟΗΓΜΕΝΩΝ ΥΠΟΛΟΓΙΣΤΩΝ

### 3η Εργαστηριακή Άσκηση/ Εργαστήριο Α - Ομάδα 5

#### Energy‐Delay‐Area Product Optimization (gem5 + McPAT)

### Βήμα 1ο

**1.** Η δυναμική ισχύς (dynamic power) καταναλώνεται από τα κυκλώματα όταν αυτά φορτίζουν και αποφορτίζουν τα χωρητικά φορτία ώστε να αλλάξουν κατάσταση, και είναι ανάλογη του συνολικού χωρητικού φορτίου, της τάσης τροφοδοσίας, της τάσης αλλαγής, της συχνότητας του ρολογιού, και του «φόρτου εργασίας».  
Τα τρανζίστορ στα κυκλώματα εμφανίζουν διαρροή (leakage), καταναλώνοντας έτσι στατική ισχύ. Το ρεύμα διαρροής εξαρτάται από το εύρος των τρανζίστορ και την κατάσταση των συσκευών. Υπάρχουν δύο μηχανισμοί διαρροής: η διαρροή κατώτατου ορίου λαμβάνει χώρα όταν ένα μικρό ρεύμα περνάει ανάμεσα από το source και το drain των τρανζίστορ που βρίσκονται σε κατάσταση off, ενώ η διαρροή πύλης είναι το ρεύμα που διαρρέεται από το gate του τρανζίστορ και ποικίλει ανάλογα με την κατάσταση της συσκευής. Με άλλα λόγια, η διαρροή είναι η ανεπιθύμητη κατανάλωση ισχύος.

Αν εκτελέσουμε διαφορετικά προγράμματα και συγκρίνουμε τους διαφορετικούς τύπους ισχύος, αυτό που θα αλλάξει από τα παραπάνω είναι η δυναμική ισχύς, εφόσον είναι ανάλογη του «φόρτου εργασίας», δηλαδή του τι εκτελείται ανά πάσα στιγμή. Επιπλέον, όπως αναφέρθηκε παραπάνω, η δυναμική ισχύς εξαρτάται από την συχνότητα του ρολογιού, κατ' επέκταση και από τον χρόνο, επομένως έχει σημασία πόσο μεγάλο σε διάρκεια εκτέλεσης είναι ένα πρόγραμμα.

**2.** Η ισχύς, γενικά μιλώντας, είναι το τι ζητάμε από την μπαταρία ανά πάσα στιγμή. Επομένως, από την στιγμή που ο δεύτερος επεξεργαστής καταναλώνει δεκαπλάσιο ποσό ισχύος από τον πρώτο, είναι αδύνατον να πετύχουμε μεγαλύτερη διάρκεια μπαταρίας με αυτόν.

Χρησιμοποιώντας το McPAT, μπορούμε να πάρουμε πληροφορίες για την καταναλισκόμενη ισχύ, μας λείπουν όμως σημαντικές λεπτομέρειες για την εκτέλεση του προγράμματος, όπως ο χρόνος εκτέλεσης, μεταξύ άλλων. Δεν μπορούμε, λοιπόν, να απαντήσουμε με σαφήνεια στο παραπάνω ερώτημα μόνο με τη χρήση του McPAT. Mε την επιπλέον βοήθεια του gem5, μπορούμε να αντλήσουμε τις απαραίτητες πληροφορίες που χρειαζόμαστε.

**3.** Όπως είδαμε παραπάνω, σε ένα σύστημα έχουμε δύο κατηγορίες καταναλισκόμενης ισχύος: την δυναμική (dynamic) και την στατική (leakage). Η δυναμική είναι η ισχύς που εξαρτάται από το πρόγραμμα (software), ενώ η στατική αφορά την ίδια την κατασκευή (hardware). 
Από την στιγμή λοιπόν που διακόπτεται η λειτουργία του συστήματος μετά την εκτέλεση της εφαρμογής, δεν έχουμε πλέον κατανάλωση δυναμικής ισχύος, έχουμε όμως κατανάλωση στατικής ισχύος (leakage), την οποία και θα εξετάσουμε.
Ανατρέχοντας στα αποτελέσματα της εκτέλεσης του McPAT, βλέπουμε τα εξής:

* **Xeon**: (Line 15) Total Leakage = **36.8319 W**
* **ARM A9**: (Line 15) Total Leakage = **0.108687 W**

Η διαρροή στον Xeon είναι πολλές φορές μεγαλύτερη από αυτήν του ARM 9.  
Επειδή αναφέρθηκε παραπάνω πως η διαρροή είναι, στην ουσία, η ανεπιθύμητη κατανάλωση ισχύος, ο ARM 9 καθίσταται περισσότερο energy efficient, παρά την διαφορά στην απόδοση.

### Βήμα 2ο

**1.** Βασιζόμενοι στο Excel worksheet που παραδώσαμε στο προηγούμενο εργαστήριο, κατασκευάσαμε ένα ακόμα worksheet στο οποίο φαίνονται αναλυτικά η επιφάνεια, η δυναμική ισχύς, η διαρροή ισχύος, η συνολική καταναλισκόμενη ισχύς, ο χρόνος εκτέλεσης, η καταναλισκόμενη ενέργεια, το EDP και το peak power για κάθε test που πραγματοποιήσαμε για κάθε benchmark. Τα αποτελέσματα αυτά τα εξάγαμε από τα αντίστοιχα αρχεία .txt που προέκυψαν με την εκτέλεση του McPAT των αρχείων .xml, τα οποία με την σειρά τους προέκυψαν με την χρήση του script GEM5toMCPAT.

**2.** Στα γραφήματα (αρχεία .png) φαίνεται το peak power για κάθε τεστ. 

(_Κατά την εξέτασή μας την ώρα του 3ου εργαστηρίου, μας προτάθηκε να συγκρίνουμε μόνο 1-2 αλλαγές παραμέτρων σε κάθε benchmark. Ωστόσο θεωρήσαμε πως η ολοκληρωμένη απεικόνιση όλων των τεστ που κάναμε στο 2ο εργαστηρίου θα έδινε πιο πλήρη εικόνα για την συμπεριφορά του peak power._)

Ένας βασικός λόγος που στα αποτελέσματα των εξομοιώσεων μπορεί να εμφανίζονται αποκλίσεις από τα πραγματικά συστήματα είναι το γεγονός ότι το McPAT δεν μοντελοποιεί με ακρίβεια ορισμένα στοιχεία, όπως SOC logic και I/O, καθώς οι αρχιτεκτονικές τους δεν είναι γνωστές. Επιπλέον, με το McPAT έχουμε high-level μοντέλα, ενώ στο επίπεδο του hardware έχουμε low-level, με αποτελέσμα να χρειαζόμαστε επιπλέον στοιχεία για να έχουμε πλήρη εικόνα του συστήματος, κάτι στο οποίο μπορεί να βοηθήσει ένας εξομοιωτής όπως ο gem5.
Υπάρχει, τέλος, και η έννοια του _silicon lottery_, που περιγράφει τις κατασκευαστικές διαφορές που δυνητικά υπάρχουν από σύστημα σε σύστημα, κάτι που συντελεί στην απόκλιση τιμών στα αποτελέσματα.

### ΠΗΓΕΣ

1. Li, Sheng, et al. "McPAT: an integrated power, area, and timing modeling framework for multicore and manycore architectures." Proceedings of the 42nd Annual IEEE/ACM International Symposium on Microarchitecture. 2009
2. Sultan, Hameedah, Gayathri Ananthanarayanan, and Smruti R. Sarangi. "Processor power estimation techniques: a survey." International Journal of High Performance Systems Architecture 5.2 (2014): 93-114
3. Triviño Valls, Josep. Power models for multicore processor simulators with multiple levels of abstraction. BS thesis. Universitat Politècnica de Catalunya, 2015
4. [https://en.wikipedia.org/wiki/System_on_a_chip](https://en.wikipedia.org/wiki/System_on_a_chip)

***

### ΚΡΙΤΙΚΗ

Το 3ο εργαστήριο ήταν το πιο ομαλό όσον αφορά την διεκπαιρέωση. Η εισαγωγή μας στο McPAT ήταν πληρέστατη με την ανάγνωση του documentation, κι η επιπλέον εμβάθυνση στηριζόμενοι πάνω στα αποτελέσματα του προηγούμενου εργαστηρίου ήταν ενδιαφέρουσα. Μας άρεσε, επίσης, το πλήθος των θεωρητικών ερωτήσεων που τέθηκαν, κάτι που ήρθε σε αντίθεση με τα προηγούμενα, περισσότερο διαδικαστικά εργαστήρια.  
Ένα θέμα που αντιμετωπίσαμε ήταν η αδυναμία του compile του McPAT στην τελευταία έκδοση Ubuntu (20.04), οπότε και έπρεπε να πάρουμε έναν pre-compiled φάκελο.

Σε γενικές γραμμές τα 3 αυτά εργαστήρια μας προσέφεραν μία καλή εξοικείωση με τον κόσμο των μικροεπεξεργαστών και την ευκαιρία να βάλουμε «κάτω από το μικροσκόπιο» την λειτουργία τους και τους μηχανισμούς τους, ακόμη κι αν αυτό έγινε στα πλαίσια της online διεξαγωγής. 
