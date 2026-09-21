```ts
type ImageSource =
  | {
  type: "imageSourceBytes";
  bytes: Uint8Array;
}
  | {
  type: "imageSourceS3Location";
  location: S3Location;
}
  | {
  type: "imageSourceUrl";
  url: string;
};
```

Defined in: [src/types/media.ts:249](https://github.com/strands-agents/harness-sdk/blob/main/strands-ts/src/types/media.ts#L249)

Source for an image (Class version).