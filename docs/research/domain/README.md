# Domain discovery checklist

Questions to answer before choosing use cases. Each area has one note in this folder.
Process: [WORKFLOW.md, Phase 0](../../../WORKFLOW.md#phase-0--domain-discovery).

| Area | Note | Status |
|---|---|---|
| A. COD cash flow | `cod-cash-flow.md` | not started |
| B. Carrier statements and fees | `carrier-statements.md` | not started |
| C. Order statuses and carrier events | `carrier-events.md` | not started |
| D. Bank statements and transfers | `bank-transfers.md` | not started |
| E. Discrepancies and complaints | `discrepancies.md` | not started |
| F. Ledger basics | `ledger-basics.md` | not started |
| G. How shops reconcile today | `shop-practice.md` | not started |
| H. Reference products | `reference-products.md` | not started |

## Sources to start from

- Carrier developer API docs: GHN, GHTK, J&T Express, Viettel Post.
- Carrier help-center pages on reconciliation and complaints, and carrier terms of service.
- Seller forums and Facebook groups for online shops.
- Help pages of Sapo, Haravan, and Nhanh.vn.
- Introductory material on double-entry bookkeeping.

## A. COD cash flow

Unlocks: glossary rows, the payout-schedule rule, the shape of the ledger.

1. Who physically holds the COD cash at each step, from the customer paying to the money
   reaching the shop's bank account?
2. What does a carrier's reconciliation period mean in practice: what closes it, and what
   is the shop sent when it closes?
3. How often does each carrier pay out, and does it differ by shop contract or amount?
4. What is deducted before payout: shipping fee, COD fee, return fee, insurance,
   surcharges? Are fees deducted from COD or billed separately?
5. When a delivery fails and the parcel returns, what happens to the COD amount and to
   the fees already charged?
6. Can money arrive before the carrier reports the order as delivered? What does the
   shop see in that case?

## B. Carrier statements and fees

Unlocks: the fee-type list, the statement-format rule, the "import a carrier statement"
use case.

7. What does one carrier statement contain: which columns, which identifiers (order
   code, waybill code, shop's own reference)?
8. In which formats is a statement delivered (spreadsheet, file download, API), and how
   do the formats differ between carriers?
9. What fee names does each carrier use, and which names from different carriers mean
   the same fee?
10. How do reweighing and remote-area surcharges appear: as a changed fee on the row, a
    separate row, or a later adjustment?
11. Can a statement correct an earlier statement? How is a correction shown?

## C. Order statuses and carrier events

Unlocks: the status list, the event-intake requirements, the idempotency check (P-5).

12. What is each carrier's list of order statuses, and which statuses are final?
13. Which statuses mean money is owed to the shop, and which mean a return is coming?
14. What does a carrier status event (webhook) contain, and what identifies one event
    uniquely?
15. Do the carriers document duplicate or out-of-order events? What do their docs say a
    receiver must do?
16. Which events carry money information: COD change, fee change, weight change?

## D. Bank statements and transfers

Unlocks: the transfer-matching use case and its tolerance rule.

17. How does a carrier payout appear on a shop's bank statement: amount, date, sender
    name, description text?
18. Does one transfer cover one statement, several statements, or part of one?
19. What in the transfer description, if anything, links it to a carrier statement?
20. In what format can a shop get its bank statement (file export, API), and which
    fields does it contain?

## E. Discrepancies and complaints

Unlocks: the discrepancy-type catalog (P-6), complaint deadlines, the complaint use case.

21. Which discrepancy types are documented or commonly reported? For each: what is
    wrong, at which step (P1–P9 in the brief) it arises, and its source.
22. For each type, what data shows it: which two values disagree?
23. What is each carrier's complaint process, and its deadline counted from which event?
24. What evidence does a carrier ask for in a complaint?
25. Which discrepancies are not errors (timing differences that resolve by the next
    period)? How can they be told apart from real errors?

## F. Ledger basics

Unlocks: the money-invariant rule (P-4), the ledger design decision.

26. What is double-entry bookkeeping, explained with one COD order as the example?
27. Which accounts does one COD order's money pass through (money the carrier owes the
    shop, fees, cash at bank)?
28. Written as a ledger rule, what must always balance for one carrier? For one order?
29. How is a correction recorded in a ledger without deleting the original entry?

## G. How shops reconcile today

Unlocks: Evidence on vision blocks W-1 to W-3, the use case actors and goals.

30. Who in a small shop reconciles COD money: the owner, staff, or an outside
    accountant?
31. What tool do they use today, and what steps do they repeat for each period?
32. What goes wrong most often, in their own words? Which problems from the brief
    (P1–P9) appear in real reports, and which never do?
33. What would they look at first if they had one view of their money?

## H. Reference products

Unlocks: the Product evidence section of each use case.

34. What do Sapo, Haravan, and Nhanh.vn offer for COD reconciliation? What do they not
    offer?
35. What do the carriers' own shop dashboards show about COD money and payouts?
36. Which gaps in these products match the problems in the brief?
