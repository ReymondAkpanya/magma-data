# Elliptic Curves in Magma

An elliptic curve E is the projective closure of a curve given by the generalised Weierstrass equation y² + a1xy + a3y = x³ + a2x² + a4x + a6.

The curve is specified by the coefficient sequence [a1, a2, a3, a4, a6]. When a1 = a2 = a3 = 0, the shorter form [a4, a6] may be used instead, giving the simplified equation y² = x³ + a4x + a6.

The curve must be nonsingular: the discriminant of the Weierstrass equation must be nonzero. The base ring of an elliptic curve must be a field; integer coefficients are automatically coerced into Q.

Elliptic curves in Magma belong to the category CrvEll. Points on a curve have type PtEll and live in point sets of type SetPtEll. The parent of a point is its point set, not the curve itself.

The category SchGrpEll is used for subgroup schemes of elliptic curves. The category SymKod stores Kodaira symbols, which classify the local structure at a prime of the Néron model of an elliptic curve over Q.

## Creating an Elliptic Curve

The primary constructor takes a sequence of Weierstrass coefficients.

```
> EllipticCurve([1, 0]);
Elliptic Curve defined by y^2 = x^3 + x over Rational Field
> EllipticCurve([1, 0, 0, 1, 0]);
Elliptic Curve defined by y^2 + x*y = x^3 + x over Rational Field
```

A curve can also be created from univariate polynomials f and h, defining y² + h(x)y = f(x). Here f must be monic of degree 3 and h must have degree at most 1. If h is omitted the curve is y² = f(x).

```
> Qx<x> := PolynomialRing(Rationals());
> EllipticCurve(x^3 + x);
Elliptic Curve defined by y^2 = x^3 + x over Rational Field
```

A curve with a prescribed j-invariant is created with `EllipticCurveWithjInvariant(j)`. For j = 1728 the curve y² = x³ + x is returned.

```
> EllipticCurveWithjInvariant(1728);
Elliptic Curve defined by y^2 = x^3 + x over Rational Field
```

A genus-1 scheme C with a rational point can be converted to an elliptic curve using `EllipticCurve(C, P)`, which returns the curve and a birational map sending P to the origin. Supplying a place instead of a point forces a Riemann–Roch computation, which is potentially more expensive.

`SupersingularEllipticCurve(K)` returns a representative supersingular curve over a finite field K.

## Checking Whether a Curve Exists

`IsEllipticCurve(s)` tests whether a coefficient sequence defines a valid elliptic curve (i.e. has nonzero discriminant). It returns a boolean and, when true, also returns the curve.

```
> ok, E := IsEllipticCurve([GF(7) | 1, 1, 0, -3, -17]);
```

## Changing the Base Ring

`BaseChange(E, K)` and `BaseExtend(E, K)` extend E to an extension field K of its base field. `ChangeRing(E, K)` uses standard coercion instead and works even when there is no ring homomorphism between the fields (for example, from Q to a finite field).

```
> K1 := GF(23);
> K2 := GF(23, 2);
> E1 := EllipticCurve([K1 | 1, 1]);
> E2 := BaseExtend(E1, K2);
> assert E2 eq ChangeRing(E1, K2);
```

`BaseExtend(E, n)` extends E to the degree-n extension of its finite base field.

## Alternative Models

Several functions return an isomorphic elliptic curve in a canonical form, together with the isomorphisms.

`WeierstrassModel(E)` returns a simplified Weierstrass form y² = x³ + ax + b. This does not apply in characteristic 2 or 3.

`IntegralModel(E)` returns an isomorphic curve over a number field with integral coefficients.

`MinimalModel(E)` returns a global minimal integral model over Q or a number field of class number 1: the discriminant has minimal p-adic valuation at every prime.

`SimplifiedModel(E)` behaves like `MinimalModel` over Q and like `WeierstrassModel` in other characteristics (except 2 and 3).

```
> E := EllipticCurve([1/2, 1/2, 1, 1/3, 4]);
> IntegralModel(E);
Elliptic Curve defined by y^2 + 3*x*y + 216*y = x^3 + 18*x^2 + 432*x + 186624 over Rational Field
> MinimalModel(IntegralModel(E));
Elliptic Curve defined by y^2 + x*y + y = x^3 - x^2 + 619*x + 193645 over Rational Field
```

The predicates `IsWeierstrassModel`, `IsIntegralModel`, `IsSimplifiedModel`, and `IsMinimalModel` test whether a curve already satisfies the corresponding condition.

## Twists of Elliptic Curves

Two curves are twists if they become isomorphic over an extension field (equivalently, they share the same j-invariant). `IsTwist(E, F)` tests this by comparing j-invariants.

`QuadraticTwist(E, d)` returns the quadratic twist of E by d. Over a finite field, `QuadraticTwist(E)` returns the unique nonisomorphic quadratic twist, whose trace is the negation of Trace(E).

`QuadraticTwists(E)` returns the sequence of all nonisomorphic quadratic twists, with E first. `Twists(E)` returns all nonisomorphic twists over a finite field, including higher-order twists for curves with nontrivial automorphisms.

```
> E1 := EllipticCurve([GF(13) | 3, 1]);
> S := QuadraticTwists(E1);
> [ IsIsomorphic(E1, E) : E in S ];
[ true, false ]
```

`IsQuadraticTwist(E, F)` returns true and an element d such that F is isomorphic to `QuadraticTwist(E, d)` if E and F are quadratic twists; otherwise it returns false.

`MinimalQuadraticTwist(E)` computes the minimal quadratic twist of a rational elliptic curve and returns the twist together with the integer d by which E was twisted to obtain it.
