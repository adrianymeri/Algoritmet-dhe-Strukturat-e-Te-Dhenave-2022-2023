## Algoritmet dhe Strukturat e të Dhënave – Java 5

---

## Notacioni asimptotik – Big-O

Një funksion $f(n)$ themi se i takon bashkësisë
$\textrm{O}(g(n))$ nëse ekziston një $k>0$ e fundme ashtu që:

$$
0 \leq f(n) \leq kg(n)
$$

Për çdo $n > n_0$ ku $n_0$ është konstante e fundme.

---

Shkallët e rritjes për dy funksione mund t'i vlerësojmë me limitin e mëposhtëm:

$$
\lim_{n\to+\infty}\frac{f(n)}{g(n)} \tag{1}
$$

Ekzistojnë 3 raste të mundshme varësisht nga vlera e shprehjes $(1)$.

---

Rasti 1:

$$
\lim_{n\to+\infty}\frac{f(n)}{g(n)} = 0
$$

Në këtë rast funksioni $f$ ka shkallë të rritjes më të ulët sesa funksioni $g$.

---

Rasti 2:

$$
\lim_{n\to+\infty}\frac{f(n)}{g(n)} = C \quad \text{ku}\ 0<C<+\infty
$$

Në këtë rast funksioni $f$ ka shkallë të rritjes të njejtë me funksionin $g$.

---

Rasti 3:

$$
\lim_{n\to+\infty}\frac{f(n)}{g(n)} = +\infty
$$

Në këtë rast funksioni $f$ ka shkallë të rritjes më të lartë sesa funksioni $g$.

---

Mund të themi që një funksion $f(n)$ i takon bashkësisë $O(g(n))$
nëse vlera e shprehjes $(1)$ del e fundme.

$$
\lim_{n\to+\infty}\frac{f(n)}{g(n)} < +\infty\ \Rightarrow\ f \in \textrm{O}(g(n))
$$

Pra për dallim nga $\textrm{o}(g(n))$ (Little-O), Big-O lejon që
funksioni $f(n)$ t'i takojë bashkësisë $\textrm{O}(g(n))$ nëse ka
shkallë të njejtë ose më të ulët të rritjes sesa funksioni $g(n)$.

---

Klasat e zakonshme të kompleksitetit që përdoren si referencë janë:

$$
\textrm{O}(1),
\ \textrm{O}(\log{n}),
\ \textrm{O}(n),
\ \textrm{O}(n\log{n}),
\ \textrm{O}(n^2),
\\\textrm{O}(n^3)
\ \dots\ \textrm{O}(n^p),
\ \textrm{O}(e^n),
\ \textrm{O}(n!)
$$

---

## Kompleksiteti kohor dhe hapësinor

Shkallët e rritjes i përdorim për të vlerësuar sa është i ngadalshëm
një algoritëm i cili përpunon një sasi të të dhënave $n$.

Kompleksiteti i ulët është më i dëshirueshëm. Pse?

---

Kompleksiteti kohor tregon rastin më të keq të hapave që duhet t'i ndërmarrë algoritmi.

Komplesiteti hapësinor tregon memorien maksimale të nevojshme për të kryer punën algoritmi.

---

**Detyrë:** Është dhënë funksioni $f(n)$ i cili e llogarit shumën e vargut $v$ me $n$ elemente.

Të tregohet kompleksiteti kohor dhe hapësinor i këtij algoritmi.

---

**Detyrë:** Është dhënë funksioni $f(n)$ i cili e llogarit shumën e matricës katrore $A_{n\times n}$.

Të tregohet kompleksiteti kohor dhe hapësinor i këtij algoritmi.

---

**Detyrë:** Janë dhënë funksionet: shuma e matricës, shuma e elementeve mbi diagonale të matricës.

Të krahasohet kompleksiteti kohor i këtyre dy algoritmeve.

---

**Detyrë:** Të shkruhen dy versione të funksionit që llogarit shumën e numrave $1\dots n$.
Versioni i parë e kryen llogaritjen me unazë.
Versioni i dytë e kryen llogaritjen përmes formulës së serisë aritmetikore.

Të krahasohet kompleksiteti kohor i këtyre dy algoritmeve.

---

**Detyrë:** Të diskutohet kompleksiteti i veprimeve mbi një varg të numrave me gjatësi $n$.

- Shuma.
- Minimumi, maksimumi.
- Plotësimi i kushtit nga një element.
- Plotësimi i kushtit nga secili element.
- Numërimi sa elemente plotësojnë kushtin.

---
