Zod Node16 Resolution Bug Reproduction:

1. Run pnpm install
2. Run pnpm build

```bash
> zod-node16@1.0.0 build /Users/samc/work/zod-node16
> tsc --build

node_modules/.pnpm/zod@3.25.17/node_modules/zod/dist/types/v4/classic/schemas.d.ts:406:28 - error TS2636: Type 'ZodObject<sub-Shape, Config>' is not assignable to type 'ZodObject<super-Shape, Config>' as implied by variance annotation.
  The types of 'keyof().options' are incompatible between these types.
    Type '{ [k in keyof { [k in keyof sub-Shape & string]: k; }]: { [k in keyof sub-Shape & string]: k; }[k]; }[keyof sub-Shape & string][]' is not assignable to type '{ [k in keyof { [k in keyof super-Shape & string]: k; }]: { [k in keyof super-Shape & string]: k; }[k]; }[keyof super-Shape & string][]'.
      Type 'keyof sub-Shape & string' is not assignable to type 'keyof super-Shape & string'.
        Type 'keyof sub-Shape & string' is not assignable to type 'keyof super-Shape'.

406 export interface ZodObject<out Shape extends core.$ZodShape = core.$ZodLooseShape, out Config extends core.$ZodObjectConfig = core.$ZodObjectConfig> extends ZodType {
                               ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

node_modules/.pnpm/zod@3.25.17/node_modules/zod/dist/types/v4/core/checks.d.ts:256:55 - error TS2304: Cannot find name 'File'.

256 export interface $ZodCheckMimeTypeInternals<T extends File = File> extends $ZodCheckInternals<T> {
                                                          ~~~~

node_modules/.pnpm/zod@3.25.17/node_modules/zod/dist/types/v4/core/checks.d.ts:256:62 - error TS2304: Cannot find name 'File'.

256 export interface $ZodCheckMimeTypeInternals<T extends File = File> extends $ZodCheckInternals<T> {
                                                                 ~~~~

node_modules/.pnpm/zod@3.25.17/node_modules/zod/dist/types/v4/core/checks.d.ts:260:46 - error TS2304: Cannot find name 'File'.

260 export interface $ZodCheckMimeType<T extends File = File> extends $ZodCheck<T> {
                                                 ~~~~

node_modules/.pnpm/zod@3.25.17/node_modules/zod/dist/types/v4/core/checks.d.ts:260:53 - error TS2304: Cannot find name 'File'.

260 export interface $ZodCheckMimeType<T extends File = File> extends $ZodCheck<T> {
                                                        ~~~~

node_modules/.pnpm/zod@3.25.17/node_modules/zod/dist/types/v4/core/schemas.d.ts:515:38 - error TS2636: Type '$ZodObjectInternals<sub-Shape, Config>' is not assignable to type '$ZodObjectInternals<super-Shape, Config>' as implied by variance annotation.
  Types of property '"~output"' are incompatible.
    Type '$InferObjectOutput<sub-Shape, Config["out"]>' is not assignable to type '$InferObjectOutput<super-Shape, Config["out"]>'.
      Type 'object | (keyof sub-Shape | keyof Config["out"] extends never ? Record<string, never> : { [K in keyof ({ -readonly [k in keyof sub-Shape as sub-Shape[k] extends OptionalOutSchema ? never : k]: output<...>; } & { -readonly [k in keyof sub-Shape as sub-Shape[k] extends OptionalOutSchema ? k : never]?: output<...>; } &...' is not assignable to type '$InferObjectOutput<super-Shape, Config["out"]>'.
        Type 'object' is not assignable to type '$InferObjectOutput<super-Shape, Config["out"]>'.

515 export interface $ZodObjectInternals<out Shape extends Readonly<$ZodShape> = Readonly<$ZodShape>, out Config extends $ZodObjectConfig = $ZodObjectConfig> extends $ZodTypeInternals<any, any> {
                                         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

node_modules/.pnpm/zod@3.25.17/node_modules/zod/dist/types/v4/core/schemas.d.ts:568:29 - error TS2636: Type '$ZodObject<sub-Shape, Params>' is not assignable to type '$ZodObject<super-Shape, Params>' as implied by variance annotation.
  Types of property '"~standard"' are incompatible.
    Type 'Props<$InferObjectInput<sub-Shape, Params["in"]>, $InferObjectOutput<sub-Shape, Params["out"]>>' is not assignable to type 'Props<$InferObjectInput<super-Shape, Params["in"]>, $InferObjectOutput<super-Shape, Params["out"]>>'.
      Type '$InferObjectInput<sub-Shape, Params["in"]>' is not assignable to type '$InferObjectInput<super-Shape, Params["in"]>'.
        Type 'object | (keyof sub-Shape | keyof Params["in"] extends never ? Record<string, never> : { [K in keyof ({ -readonly [k in keyof sub-Shape as sub-Shape[k] extends OptionalInSchema ? never : k]: input<...>; } & { -readonly [k in keyof sub-Shape as sub-Shape[k] extends OptionalInSchema ? k : never]?: input<...>; } & Para...' is not assignable to type '$InferObjectInput<super-Shape, Params["in"]>'.
          Type 'object' is not assignable to type '$InferObjectInput<super-Shape, Params["in"]>'.

568 export interface $ZodObject<out Shape extends Readonly<$ZodShape> = Readonly<$ZodShape>, out Params extends $ZodObjectConfig = $ZodObjectConfig> extends $ZodType {
                                ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

node_modules/.pnpm/zod@3.25.17/node_modules/zod/dist/types/v4/core/schemas.d.ts:694:36 - error TS2636: Type '$ZodEnumInternals<sub-T>' is not assignable to type '$ZodEnumInternals<super-T>' as implied by variance annotation.
  Types of property 'output' are incompatible.
    Type 'sub-T[keyof sub-T]' is not assignable to type 'super-T[keyof super-T]'.
      Type 'keyof sub-T' is not assignable to type 'keyof super-T'.
        Type 'string | number | symbol' is not assignable to type 'keyof super-T'.
          Type 'string' is not assignable to type 'keyof super-T'.

694 export interface $ZodEnumInternals<out T extends util.EnumLike = util.EnumLike> extends $ZodTypeInternals<$InferEnumOutput<T>, $InferEnumInput<T>> {
                                       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Found 8 errors.
```
