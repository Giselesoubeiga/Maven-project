Yes — for the queues I’m using Fn::ImportValue. When I was doing my research, I saw that those come directly from the SQS child stack, and the workers need those queue ARNs to register correctly.

The security groups are different because those are passed down from the Evaluation stack as parameters, so in the worker template I just reference them with Ref.
