Implicit sub-classes
====================

Let's say we are modeling automobiles. Consider two options:

1. One class for Automobile, with a single set of properties, like manufacturer, model, color, etc.
2. One class per manufacturer, each with its own set of properties.

Which is better? Cars from different manufacturers have more commonalities than differences. (1) is better, because it better ensures standardization of property names across Automobile instances, which eases comparability.

Do contracting procedures have more commonalities than differences? We believe so. To promote standardization and comparability, it is better to use the same class for all procedures, as much as possible.

That said, there are differences. To model differences, instead of choosing between different classes, there are several options that better achieve standardization:

1. Have one "big" class that has all properties for all procedures.

   -  This is simple for data users, as they only need to look up the reference for one class, and the same concept is always expressed using the same property of that one class. It also ensures standardization, since there is no possibility of two classes having different properties for the same concept.
   -  This, of course, also makes it possible for data to be incoherent (e.g. publishing a justification for a direct award, as part of an open procedure). Systems would need rules to ensure data is not incoherent – but systems always need some rules, e.g. to ensure start dates are before end dates. With this option, they'll simply need more.

2. Have a "basic" class with properties common to all/most procedures, with subclasses for specific procedures.

   -  Let's say we are also modelling motorcycles. We could have one "big" class for vehicles. If our use case is counting all the vehicles in use in a region, as part of an analysis to support transport decisions, this option works. If our use case is selling vehicles, it's better to have separate classes with different properties for motorcycles and cars, given that most buyers are either looking for one or the other and are not comparing between the two. Standardizing, e.g. fuel efficiency and carbon emissions, across both classes is not important to this use case (though it is relevant to the first use case).
   -  This option is often chosen by semantic 'purists'. It strikes a different balance between the correctness and complexity of the model. For contracting, it segments different procedures into different classes, giving a feeling of having a clean model. However, it also opens the door to subclasses diverging over time. For example, for government leases, one might choose the terms "lessor" and "lessee". However, these terms are modeling the same concepts as "buyer" and "supplier" or "contracting authority" and "economic operator." If every procedure uses its own jargon for the same concepts, standardization is weaker and use is harder.
   -  In practice, once data is serialized, this option often looks the same as (1). In terms of serialization, you can either:

      1. Introduce instances of different classes using different keys. Instead of ``"tender": {…}`` you'd have ``"openProcedure": {…}``, ``"directAward": {…}``, etc. This is bad, because data users now need to learn however many classes a given publisher implements. Instead of there being one place to find the submission period, there might be a dozen.
      2. Introduce instances of different classes (with the same superclass) using the *same* key. That is: ``"tender": {…}`` for all procedures. Some objects will have different fields because they are instances of different classes. The data will look the same as in (1) (as long as there have been no divergences between classes). To preserve the class information, a single field can indicate the class name, e.g. ``"procedureType": "directAward"``; this can equally be done in (1) with a change in perspective: describing the procedure type rather than preserving the class name.

   -  Given that, in practice, this option looks the same in JSON as (1), the only reason for pursuing it is to satisfy a desire for purity in modeling.

3. Have different classes for different procedures, with no class hierarchy.

   -  This is the worst option, because it offers no mechanism to ensure any degree of standardization across classes.

An important point is that having no standardization at all offers the maximum flexibility (e.g. everyone uses whatever terms they like); standardization is about reducing flexibility, and the challenge is to find a way to do so without limiting use cases.
