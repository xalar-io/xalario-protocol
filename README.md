# Xalar.io

Xalar.io is an open source protocol that enables easy and flexible payment contracts based on blockchain for customers, employers and workers.

## Abstract
We believe that every person in the world should have the opportunity to participate in the economy and contribute to society. Therefore we want to provide easy to use tools based on blockchain so as to remove political and social barriers.

Workers are key players in any economy and should be protected. Clear rules based on smart contracts give people a powerful tool to work without worries, knowing their rights from the start of a contractual relationship.

Companies hiring people because they live near the working site is an outdated paradigm. With the tools of modern society, it should be obvious that qualified people should be hired no matter their location. Clear hiring rules and automated processes provide companies the reliability they need.

In the following sections, we aim to describe the protocol that can be a game changer for people and companies all around the world.

## Specification
![Xalar.io Protocol](https://res.cloudinary.com/vonpix-srl/image/upload/v1569770396/Alternativas_protocolo_o3y6hh.png "Protocol")

The protocol is kept simple but flexible enough to allow various use cases to be implemented (from the common ones to the ones more complex).

### Parties involved
There are two key parties involved in this protocol:
 - The hiring party that is willing to pay an amount of money for a service based on pre-established rules, henceforth referred to as 'company'.
 - The hired party that is willing to provide a service in exchange for payment, or series of payment, based on pre-established rules, henceforth referred to as 'worker'.

### Contracts
This protocol proposes the following set of smart contracts:
 - The `Company Pool` that should hold the funds to provide to all the `Work Agreements`, which should have been previously authorized. The main motivation is to simplify the process for the company and manage only one source of funding to the work agreement. The main responsibility of this contract is to manage the fund, communicate with the agreements and do the right transfers to the workers whenever is required.
 - The `Work Agreement` should have a common interface but implement the logic that each work agreement needs. Each agreement should be assigned to only one worker. Both the worker and the company should have a set of methods that allow each party to interact with it as needed.

 #### Work Agreement
*DRAFT* - The variables and functions detailed below MUST be implemented.

**`company` variable**

The address of the hiring party.

**`worker` variable**

The address of the hired party.

**`companyPool` variable**

The address of the `Company Pool` contract from which this contract will request funds as the hired party collect the result of their work.

**`isActive` variable**

A boolean indicating if the agreement is active or not.

**`paymentScheme` variable**

The implemented payment scheme. This generalization allow many types of schemas to be implemented using the same standard interface. Some examples are listed below:

`"TIME_BASED"`: This is a traditional scheme based on time that the hired party works.

`"PRODUCTION_BASED"`: In this scheme the worker is payed based on the amount of a certain goods that produces.

**`paymentAmount` variable**

This is the amount the hiring party will pay the hired one based on the `paymentScheme`. It should always be the minimal unit that the scheme determined. For example, for a `"TIME_BASED"` contract that pays hourly, this amount should be the amount to be paid for one hour of work.

**`startDate` variable**

Timestamp in which the agreements starts.

**`endDate` variable**

Timestamp in which the agreements ends. It could be `null` if it's not required per the agreement between parties.

**`collect` function**

Only to be executed by the hired party. This function should invoke the `Company Pool` and request the funds that the work can collect to be transferred to the worker address.


 ### How it works
 1. The Company creates a `Company Pool` that it should fund. The size of this pool should always be at least the amount that all `Work Agreements` could collect at any given time. It's the company responsibility to monitor the size of this pool and fund it whenever it's necessary. A simple backend server could easily track this pool and trigger funding mechanisms when needed.
 2. The Company and the Worker set the rules of the `Work Agreement` and then create the required contract.
 3. As the Worker requires, based on the conditions set in the agreement, it should be able to collect the result of their work. Also the Worker could monitor the health of the `Company Pool`.
 4. Whenever it's needed, both parties can either terminate the agreement or updated as required.


## Next steps
1. Refine the protocol and validate with the community and future users.
2. Create a `Work Agreement` factory dApp to allow anyone to create agreements without the need of code.
3. Integrate with wallets to simplify access to the smart contracts for workers.
4. Search for partners to make this protocol an industry standard.

## Authors
- Mateo Castro <mateo@xalar.io>
- Ramiro Gonzalez <ramiro@xalar.io>

