This document provides the steps you need to take to update the reference assembly when adding new **public** APIs to an implementation assembly (post [API Review](adding-api-guidelines.md)).

## For most assemblies within libraries

1. Implement the API in the source assembly and [build it](../workflow/building/libraries/README.md#building-individual-libraries).
2. Run the following command (from the src directory) `msbuild /t:GenerateReferenceSource` to update the reference assembly**.
3. Navigate to the ref directory and build the reference assembly.
4. Add, build, and run tests.

** **Note:** If you already added the new API to the reference source, re-generating it (after building the source assembly) will update it to be fully qualified  and placed in the correct order. This can be done by running the `GenerateReferenceSource` command from the ref directory.

## For System.Runtime

These steps can also be applied to some unique assemblies which depend on changes in System.Private.Corelib. (partial facades like System.Memory, for example).

1) Run `dotnet build -c Release /t:GenerateReferenceSource` from the System.Runtime/ref directory.
2) Filter out all unrelated changes and extract the changes you care about (ignore certain attributes being removed). Generally, this step is not required for other reference assemblies.
