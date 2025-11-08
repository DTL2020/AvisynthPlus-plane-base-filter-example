# AvisynthPlus-plane-base-filter-example
Example of planes-based processing in AVS+ filtergraph

New filter API functions (used):

class IClip {
  virtual bool __stdcall SupportPlaneOutput() = 0; // To check if filter support plane output mode
  virtual void* __stdcall ProcessPlaneOfFrame(int n, AvsPlane p, ROWS_REGION rr, IScriptEnvironment* env) = 0; // To request processing of planes after first
  virtual PVideoFrame __stdcall GetPlaneOfFrame(int n, AvsPlane p, ROWS_REGION rr, IScriptEnvironment* env) = 0; // To connect filters via caches in filtergraph and process first plane

Implementations of virtual methods for most filters (some require same in the classes or cause instantination errors)
// instantiable null filter
class GenericVideoFilter : public IClip {
  bool __stdcall SupportPlaneOutput() { return false; }
  PVideoFrame __stdcall GetPlaneOfFrame(int n, AvsPlane p, ROWS_REGION rr, IScriptEnvironment* env) { return 0; }
  void* __stdcall ProcessPlaneOfFrame(int n, AvsPlane p, ROWS_REGION rr, IScriptEnvironment* env) { return 0; }

  
